---
layout: post
title: Cara Mudah Membuat Drag And Drop Table Pada Laravel
github: https://www.nicesnippets.com/blog/laravel-6-drag-and-drop-datatable-rows-for-sorting-example
image: https://www.nicesnippets.com/upload/blog/1578747903_sort.png
language: php | Laravel
---

### 1. Menambahkan Depedency
Di sini kita perlu menginstall depedency pada node module.
```bash
npm install jquery-ui
```
kemudian tambahkan require jquery pada `resources/js/app.js`.
```bash
require('jquery-ui/ui/widgets/sortable');
```

### 2. Menambahkan Script pada `resources/js/custom.js`.
```bash
var fixHelper = function(e, ui) {
    ui.children().each(function() {
        $(this).width($(this).width());
    });
    return ui;
};

$( "#tablecontents" ).sortable({
    items: "tr",
    cursor: 'move',
    helper: fixHelper,
    update: function() {
        sendOrderToServer();
    }
});

function sendOrderToServer() {
    var order = [];
    var token = $('meta[name="csrf-token"]').attr('content');
    $('tr.row1').each(function(index, element) {
        order.push({
            id: $(this).attr('data-id'),
            position: index + 1
        });
    });
    
    $.ajax({
        type: "POST", 
        dataType: "json", 
        url: "/admin/post/sort-update",
        data: {
            order: order,
            _token: token
        },
        success: function(response) {
            console.log(response);
            window.location.reload();
        }
    });
};
```

Production
```bash
npm run prod
```

### 3. Menambahkan Script pada View
```bash
<tbody id="tablecontents">
    @foreach($posts as $post)
    <tr class="row1" data-id="{{ $post->id }}">
        <td class="pl-3"><i class="fa fa-sort"></i></td>
        <td>{{ $post->title }}</td>
        <td>{{ date('d-m-Y h:m:s',strtotime($post->created_at)) }}</td>
    </tr>
    @endforeach
</tbody>
```

### 3. Menambahkan Script pada Controller
```bash
class PostController extends Controller
{
    public function index()
    {
        $posts = Post::orderBy('order', 'ASC')->get();

        return view('post',compact('posts'));
    }

    public function sortUpdate(Request $request)
    {
        $posts = Post::all();

        foreach ($posts as $post) {
            foreach ($request->order as $order) {
                if ($order['id'] == $post->id) {
                    $post->update(['order' => $order['position']]);
                }
            }
        }
        
        return response()->json(['success' => 'Update Successfully.']);
    }
}
```

### 3. Menambahkan Script pada Route
```bash
Route::post('post/sort-update', 'PostController@sortUpdate', ['as' => 'admin'])->name('admin.post.sort-update');
```

Sekian untuk kali ini semoga bermanfaat :D untuk lebih lanjut bisa kunjungi [link](https://www.nicesnippets.com/blog/laravel-6-drag-and-drop-datatable-rows-for-sorting-example) tersebut.
