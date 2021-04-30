---
layout: post
title: Cara Mudah Membuat Search Delegate Pada Flutter
github: https://medium.com/codechai/implementing-search-in-flutter-17dc5aa72018
image: https://miro.medium.com/max/338/1*2x5MBA3_5vyomOrWhCMn2w.png
language: dart | flutter
---

Memastikan possible untuk penelusuran pencarian data melalui `showSearch` dari data asset pada json.

### 1. Membuat Search Delegate
#### Contoh
susunan directory
```bash
❏ lib
    ❏ page
        ❏ train_page.dart
        ❏ components
            ❏ station_widget.dart
            ❏ station_search_delegate.dart
    ❏ model
        ❏ station.dart
        ❏ station_lookup.dart
    ❏ main.dart
❏ assets
    ❏ data
        ❏ stations.json
```

`assets/data/stations.json`
```bash
[
  {
    "station_code": "BD",
    "station_name": "BANDUNG"
  },
  {
    "station_code": "BKS",
    "station_name": "BEKASI"
  },
  {
    "station_code": "BOO",
    "station_name": "BOGOR"
  },
  {
    "station_code": "WT",
    "station_name": "WATES"
  },
  {
    "station_code": "YK",
    "station_name": "YOGYAKARTA"
  }
]
```

tambahkan pada `pubspec.yaml`
```bash
assets:
     - assets/data/stations.json
```
kemudian jalankan
```bash
flutter pub get
```

`lib/main.dart`
```bash
import 'package:flutter/material.dart';
import 'package:flutter/services.dart' show rootBundle;
import 'package:my_app/page/train_page.dart';
import 'package:my_app/model/station.dart';
import 'package:my_app/model/station_lookup.dart';

import 'dart:convert';

void main() async {
    WidgetsFlutterBinding.ensureInitialized();
    
    List<Station> stations = await StationDataReader.load('assets/data/stations.json');
    runApp(MyApp(stations: stations));
}

class StationDataReader {
    static Future<List<Station>> load(String path) async {
        final data = await rootBundle.loadString(path);
        return json.decode(data).map<Station>((json) => Station.fromJson(json)).toList();
    }
}

class MyApp extends StatelessWidget {
    MyApp({ this.stations });
    
    List<Station> stations;
    final appTitle = 'Search Delegate Demo';
    
    @override
    Widget build(BuildContext context) {
        return MaterialApp(
            title: appTitle,
            theme: ThemeData(
                primarySwatch: Colors.blue,
            ),
            home: TrainPage(appTitle: appTitle, stationLookup: StationLookup(stations: stations)),
        );
    }
}
```

`lib/model/station.dart`
```bash
class Station extends Object {
    String station_code;
    String station_name;
    
    Station({this.station_code, this.station_name});
    
    factory Station.fromJson(Map<String, dynamic> json) {
        return Station(
            station_code: json['station_code'],
            station_name: json['station_name'],
        );
    }
}
```

`lib/model/station_lookup.dart`
```bash
import 'package:my_app/model/station.dart';

class StationLookup {
    StationLookup({ this.stations });
    final List<Station> stations;
    
    List<Station> searchString(String string) {
        string = string.toLowerCase();
        
        final matching = stations.where((station) { return station.station_code.toLowerCase() == string || station.station_name.toLowerCase() == string; }).toList();
        if (matching.length > 0)  return matching;
        
        return stations.where((station) { return station.station_code.toLowerCase().contains(string) || station.station_name.toLowerCase().contains(string); }).toList();
    }
}
```

`lib/page/train_page.dart`
```bash
import 'package:flutter/material.dart';
import 'package:my_app/page/components/station_widget.dart';
import 'package:my_app/page/components/station_search_delegate.dart';
import 'package:my_app/model/station.dart';
import 'package:my_app/model/station_lookup.dart';

import 'dart:async';
import 'dart:convert';

class TrainPage extends StatefulWidget {
    TrainPage({ this.appTitle, this.stationLookup });
    
    final StationLookup stationLookup;
    String appTitle;
    
    @override
    _TrainPageState createState() => new _TrainPageState(appTitle: appTitle, stationLookup: stationLookup);
}

class _TrainPageState extends State<TrainPage> {
    _TrainPageState({ this.appTitle, this.stationLookup });
    
    String appTitle;
    final StationLookup stationLookup;
    
    Station departure;
    Station arrival;
    
    Future<Station> _showSearch(BuildContext context) async {
        return await showSearch<Station>(
            context: context,
            delegate: StationSearchDelegate( stationLookup: stationLookup )
        );
    }
    
    void _selectDepart(BuildContext context) async {
        var station = await _showSearch(context);
        setState(() => departure = station);
    }
    
    void _selectArrival(BuildContext context) async {
        var station = await _showSearch(context);
        setState(() => arrival = station);
    }
    
    @override
    Widget build(BuildContext context) {
        return Scaffold(
            appBar: AppBar(
                title: Text(appTitle),
            ),
            body: Container(
                padding: const EdgeInsets.all(8.0),
                child: SafeArea( // form
                    child: Column(
                        children: <Widget>[
                            StationWidget(title: 'KEBERANGKATAN', station: departure, onPressed: () => _selectDepart(context)),
                            StationWidget(title: 'TIBA', station: arrival, onPressed: () => _selectArrival(context)),
                        ],
                    ),
                ),
            ),
        );
    }
}
```

`lib/page/components/station_widget.dart`
```bash
import 'package:flutter/material.dart';
import 'package:my_app/model/station.dart';

class StationWidget extends StatelessWidget {
    StationWidget({ this.title, this.station, this.onPressed });
    
    final String title;
    final Station station;
    final VoidCallback onPressed;
    
    @override
    Widget build(BuildContext context) {
        return InkWell(
            onTap: onPressed,
            child: Padding(
                padding: EdgeInsets.symmetric(horizontal: 16.0, vertical: 8.0),
                child: Row(
                    mainAxisAlignment: MainAxisAlignment.spaceBetween,
                    children: <Widget>[
                        Text( title ),
                        Text( station != null ? '${station.station_name} (${station.station_code})' : '---' ),
                    ],
                ),
            ),
        );
    }
}
```

`lib/page/components/station_search_delegate.dart`
```bash
import 'package:flutter/material.dart';
import 'package:my_app/model/station.dart';
import 'package:my_app/model/station_lookup.dart';

class StationSearchDelegate extends SearchDelegate<Station> {
    StationSearchDelegate({ @required this.stationLookup });
    
    final StationLookup stationLookup;
    
    @override
    Widget buildLeading(BuildContext context) {
        return IconButton(
            tooltip: 'Back',
            icon: AnimatedIcon( icon: AnimatedIcons.menu_arrow, progress: transitionAnimation, ),
            onPressed: () { close(context, null); },
        );
    }
    
    @override
    Widget buildSuggestions(BuildContext context) {
        return buildMatchingSuggestions(context);
    }
    
    @override
    Widget buildResults(BuildContext context) {
        return buildMatchingSuggestions(context);
    }
    
    Widget buildMatchingSuggestions(BuildContext context) {
        if (query.length < 3) return Container();
        
        final searched = stationLookup.searchString(query);
        
        if (searched.length == 0) return StationSearchPlaceholder(title: 'No results');
        
        return ListView.builder(
            itemCount: searched.length,
            itemBuilder: (context, index) {
                return StationSearchResultTile( station: searched[index], searchDelegate: this, );
            },
        );
    }
    
    @override
    List<Widget> buildActions(BuildContext context) {
        return query.isEmpty ? [] : <Widget>[
            IconButton(
                tooltip: 'Clear',
                icon: const Icon(Icons.clear),
                onPressed: () { query = ''; showSuggestions(context); },
            )
        ];
    }
}

class StationSearchPlaceholder extends StatelessWidget {
    StationSearchPlaceholder({@required this.title});
    final String title;
    
    @override
    Widget build(BuildContext context) {
        final ThemeData theme = Theme.of(context);
        return Center(
            child: Text( title, style: theme.textTheme.headline, textAlign: TextAlign.center, ),
        );
    }
}

class StationSearchResultTile extends StatelessWidget {
    const StationSearchResultTile({ @required this.station, @required this.searchDelegate });
    
    final Station station;
    final SearchDelegate<Station> searchDelegate;
    
    @override
    Widget build(BuildContext context) {
        final title = '${station.station_code}';
        final subtitle = '${station.station_name}';
        final ThemeData theme = Theme.of(context);
        return ListTile(
            dense: true,
            title: Text( title, style: theme.textTheme.body2, textAlign: TextAlign.start, ),
            subtitle: Text( subtitle, style: theme.textTheme.body1, textAlign: TextAlign.start, ),
            onTap: () => searchDelegate.close(context, station),
        );
    }
}
```

Sekian untuk kali ini semoga bermanfaat :D untuk lebih lanjut bisa kunjungi [link](https://medium.com/codechai/implementing-search-in-flutter-17dc5aa72018) tersebut.
