---
layout: post
title: Cara Mudah Upload Gambar Dengan Tiny MCE Pada Laravel
github: https://kevinchoppin.dev/blog/implementing-simple-file-uploads-in-tinymce-editor
image: data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wCEAAkGBxMSEhUTExMWFRUVFhgYGBUVFxUXGRYZGRUXGBcVGBcYHCggHRolHRgXITEhJSkrLy4xFx8zODMsNygtLi0BCgoKDg0OGg8PFS0dHR4tMTc3Nys3LS0yNysrKy0tLS0rLTctKzcrLS04KystODcsNystNy4rLS8vLTcrLTMrLf/AABEIAKMBNgMBIgACEQEDEQH/xAAbAAEAAQUBAAAAAAAAAAAAAAAABQECAwQGB//EAEYQAAEEAAQEAwQECggGAwAAAAEAAgMRBAUSIRMxQVEGImEycYGRFFLR4QcjQmJzgqGisbIWMzRTwcLD8BUkQ5LT8SV0s//EABoBAQACAwEAAAAAAAAAAAAAAAABAgMEBgX/xAAuEQEAAQIDBQcDBQAAAAAAAAAAAQIRAwQhBRIzcbETFDI0UoHhIiNRFTFhkfD/2gAMAwEAAhEDEQA/APcUREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBEQlARROMz+JmzfOfTl/3fZaipfEUp5BrR7iT8yf8ABRvQ0cXaOBhzbevP8aurRcgM/n7tP6qqo3oYf1bA/E/73dciIrPUEREBERAXN4nxxg43yMc6QcJ5Y9whmc1rmmiC5rSF0i8ughne3NBHiooIjisQHtkYCXW0aiJC7ygt29k1uUHp0EzXta9hDmuAc1w3BBFgg9iFrY3M44nxMeSHTOLGU1xBcBe5AobDquP8NZxc2BY24YH4BxELnWNTHtaPMd3ENB36jdYMpzyd/wBEPGc5smPxDCbFPjaJCxvL2RQpB2eR5szFR8VjXNGt7KfQNseWE7EirGyQ5sx2Jkwwa7XHGyQuNaSHlwAG935ey8+yvGyCHC4Zkxw7MTi8YJJm6dTdEjnNjaXCg55NA+nwM14VjLMzxbDOcRoghbrdp1DzOOh5aAC4XzrqEE9nHifD4aQRSF+tzNYayKSTy2W35GnqFt5Pm8OKj4kD9bbLTsQWuHNrmuAIO42I6hcnnzZTm7ODMyF/0E+eRmttcfdunU3e6N30Khoc4kw+HxDIjqldmDY5sTEWEPMw1OfHrqNjvKGUfK0kG0HqaLz+HNsRhm4o4g4mOBsLXNfI/CTYiKVz9DQ0McQQ7UCNYq2notZuaYqGTExF2Ib/APHzTtbiJIJJGPYaa9pi2aDZ8p6hB6So/H5zDFDJO54McRp5ZchadQaWkMs2CRY6Lljm8khymNuIcDiIn8UsLdTv+VvWdjRD7PvCgcGJcPgMxnjxMuuOedgBLK1CaO5iNN8QjnvXmOyDvsX4hazEx4ZkUsskjBIdAbpjjL9AkeXOG13sLOx25KZXAHBP/wCLSOE81jBiWrZyMrgIfZ/qwdwOd9VZhc/ldhMqdxyZJsRG2U23U9vnDw4dr0g/BB2WTZuzEtkcxrmiOWSI6q3dG6iRRPlPTr6LUzbxTh8PJwXF75a1cOGN8rwO7gwGunPutH8H/wDV4r/72J//AEWp4ImYzE5hHKQ3EHFPf5qDnQkDhEXzaBfu1Dug6fJ81ixUYlhdqbZG4LSHNNOaWuAIIK3Vx/iHOuLLhcPh8S2OOaSZss8RYS10bQeCHGw17i7rvyrnvCZtnWJw8OYQsxLpfoxwxjnOnW3iytD4nuaAHGr3q9z8A9LJWPDztkaHsc17Tyc0hwPuI2K4vg4hmNkwbsZM9kuEM2s8MPZI2ZrTw6ZQaRY011+Kgspxc2GyrCuhlld9JljiIBh/EN1S6hCXgNa5xGm3kgE9EHqqLzbGZljYMPjrMzGxxMfG6aTDyTRvLwHNuJx8rm7jUOhUlHFiGYxmHdjJntxWGke534sGKRrmeaLy00b0GkH1tB2WHxDJGhzHNe03TmkOBo0aI25gj4KMxmftZimYVsUkkjmh7iwN0xML9Gt5c4bXews7KC/BThS3BNfxXuDjIOES3RHpmkBLQBYLuZsn0pak+FfHmuIkbNM8x4TjBls8/wCMkLcP7N8MHkOfqUHoCLzWPMp48NhccMc6aSeSIOw54fDfxHAOhjYBbXtvnZ9kqa8NiefFYl78TJw8Pi5GMhGkNcNA2eastGoUARRF7oOwRFZLIGgucaA3JKImbaySyBoLnGgNySuRzbNnSkhtiPt9b1d9ipnGamY0NmDkO/qfsUcFWZc5n9oTiz2eHP09fhWlRVCqqPKWolIoHoaIizO5EREBERAUNP4VwT3mR+Fhc9xLi5zGkkk2Sb57qZRBHZlkeGxAYJoI5BH7Ac0HTy2HpsNuWwV0WTYdunTCwaHukZTQNL3XqeOxNn5rfRBHS5FhnRGF0EZiLi7QWitRJJcOzrJ39SrstybD4feGFkflDfI0C2gkgGue5J+K3XuoE9hey4LE+MziMNj2sbJE+JsvCeGSsprWNILnEDRJZ9k0duSDrczyDC4hwdPBHK4CgXtBIFk1v6k/NZY8ow7YjAIYxCecQY3Qb522qKivD3iiCYxwB7+KYg4F7HtEgAGpzHuFP36jnuRay4fxbhXvaxrn1I7RHKY5BDI/fyMlLdLjsa3o1taDZwnhzCRRvjZh4msk2e3QPOOgdfMDp2VcB4fwsBuKCNh0lthostdWoE9QdLefYKP8bZhLho4p436WRzx8cU0h0LnaXcwSNy3cUo3MvEczMzYxrv8AlWPiw8opu807HuYdVWAPxYO/5XrsE/gfDWEhcHxYaJjmuLg5rQCCWlpIPuJHxKSeGsI50jzh4y6YESHSPOC4OId3tzQT3IUTgfEVTY2aaWsPFMzDwsDbJka38YGhrdb3Oc4AAXyK1/FniNsmX4s4d8sU0Qj1Nc18MseqRuk04AgEXRGx3QdY3BRiTihjeJoDNdebQDYbfa91oYfwxg2P1sw0TXaw/UGAEObdEdqs8lhy3xZhppWwtc8PeCYy+ORjZQBZMbnABwrfb3qQxeaRxSwwvJD5y4R7EgljdRBdyBrlfNBmwmDjiDhGwMDnOe4NFW5xtzj6krTzbIMLiqM8DJCNgXDcDtqG9ei1m+LMIWYiTieXCuLZTpd5SCRsK81kECuahc18VHCsxkokdO5kjGsidC5jYCWNdoe9o3BBvUa3oc0HSOyDCmH6OcPFwQbEehukH61fW9eaR5BhWwnDtgjEJIJjDRpcQQQSOpsDc9guZx/ihoxeEk1TNhfDPcXDmDnva5gb+JrUTzo1ys8l1WTZtFiohLC7U0kjcFpBBotLTuCEGc4KPiibQ3iBmgPrzaCdRbfa91o4fw3hGNkY3DxBs1cRukaX1dW3ltZrsuXzOLHx4zDYcZi+sTxjq4GH8nDaHAAad7uvgpSHNPosk/0jGOlEEETns4AbpsuHF1MHmLvqjlSCUw/hvCRxvhZh4xHJ7bQ0U+uWrvXqt12CjMjZCxutjS1r63a01bQexofJQ8HjLCPMgDn3HG6XeKQa4285I7b52+7n0tbv/HoKw5DifpX9TQJLho1kkVsA3c3yQZMvybDwPkfDCyN0pt5aK1USRfxJ+a2Bg4xIZtA4haGF9eYtBsNvtZJWdEEVh/DeEjl47MNE2WydYYAQTzI7H1Hdb2FwccZeWMa0yOL30K1OIALj3Ow+SzqyaVrGlziAALJPRETNtZJZA0FzjQG5JXH5xmpmNDZg5Dv6n7Fbm2aunO1iMHyt7/nO+zotBqiXO5/P9r9vDn6evwBVAVQqhVl5SoCrSBUe6lUWvd0CLGihW70ZERZndCIiAiIgIiICIiAuGnyPF6cygbExzMWZZI5eIBTnsa0RllX09q13KIOVxmQSPmwLqAZBBPHKQQCDJCxjdI67gqFyjwjOwwQywl7IXtJl+mz8MhhtjmYbk191ty2O++3oiINDP8uGJw00B/6kbmi+hI8p+Bo/BcxhPCs3/DJYZCPpUrzMXarHFa4GLze6Ng+a7ZEHCzeEJjgcOywcRFMcQ8cR0fEe8vMjRKzdrqfQcPqjutfEeE5pcLixwTHNM2NjOJi5MQ4tbIHHW5+wqjVdz8fQkQcgcvxuIxGG48UMMeFeXl8cheZXBha0MbpBY3eyCpLxjlck8LTBXHhljmi1Ghqa7cE9i0uFKdRB58PBErXYZrS3hOZEMZZ9t8MhmDh9bU9zgfRbmZeGZ5YszYNIOKex0Vu56WM2PbdpC7VEHL4bA4mXFYXEywti4cUzHtEgfRcW6CCALsA+61t+Esrkw7cQJABxMXPK2jfke4Ft9j6KdRBA5tlckmPwU7QOHAMQHkmiOJGGtoddwonxH4cnmfjywNrEYaKOO3AW5jnF19hvzXaIg53EZS84zCzU3hxQSxvsjm4MoV1GxUD4EysjFTeYPgwTpIMORuBxX8SQX1c0FrLXd4vDMlY6ORocx4LXNPJwIog+ix5fgIoGCOGNsbBya0ADfmfeg2URWTStY0ucQABZJ6IiZtrJNK1jS5xAAFknouJzfNnYh1CxE07D6x7n7OiszvOHYh2ltiMHYd/znfZ0WoxtbKbOcz+f7Wezw/D1+F6qqKoUS8tUKoVEVJF4WFxtJH9FbqVJlWZVRUtVUD0ZERZ3dCIiAiIgIiICIiAiIgIiICIiAiIgIiICIiAiIgIiICIrJpQxpc4gACyT0REzbWSaVrGlziA0CyT0XCZ7nJndQsRjkO/5zvs6K/Pc2OINCxGDsO/5zvs6KLjj39FaznM/n5xft4fh6/DJCyt1lQNVwCPLUCuARXBVkA1VJoIsOIf0VZ0RLET1VysVWlYVFyIiJekoiLYd2IiIMb5KskgAECz61W99ykb9XJwPu3/xVHsDrBFiwaPpRH7QFZh8M2O9DA3Vua6oKsxLSQA9hJ5AEG7uq39D8irzILrU2+3Xp6+o+awQYGNhtrKI2u+wrv2V02DY+y5gN1d9auv4lBkZIDsHNJFHbfY8jz60VRswPJ7T7vcD39R8wqQwtYPK2hsNveT/ABcfmsMmWxO5xNN3+1xcf2k/MoNl8gHNzRz57cufVWmdou3t257jbve6TQtf7Tbrl3HLkeh2G6wuy6I0OGNqHbYcht2oIM8kobWpzRewvazV0LPYH5IyUO5Oafdv/iqTwteNLm2O3wI/gSsWHwcbHFzWAOqr61tt/vkgy8dtka22NiNrHLY7/nD5hXB9iw4V36fO1hmwbHm3Ms8+fpXftY9xI6lXsw7Q3QGeXfy8xvueaC5swJoPaT6e6x1V9HuPl961YcvjY4ObGGkXVbcxXK66Lav0QKPcfL70o9x8vvS/RL9ECj3Hy+9KPcfL7019a/gqOkAFnYdyQgrR7j5felHuPl96o2S+W99iFW/RAo9x8vvSj3Hy+9L9Ev0QKPcfL71HZtlP0ig6VzWj8ltUT3Ng2pG/RA70RTEw6cSndqi8Od/ohH/eyfu/Yrm+E2D/AKr/AN37F0F+iX6Kby1u4Zf0QgB4UZ/ev/d+xV/osz+8f+79inr9Ev0UHcMv6IQX9F2f3j/3fsT+i7P7x/7v2Kdv0QO9EO4Zf0Q4/OsvbhyynF2oOJuttOnt71Ck2bXQ+NnbwjuH/wCRc6Fjqc5n6KcPMVUUxaIt0hVERY2kuBRW2iJZJ/HuIJ8rIm+8OcfnqH8EZ48xI3LInDqKc0/PUf4Llmq4Lp5y2F+27D0u+Y9778vQsq8ewSENlaYSepOpn/cNx8QB6rq43hwBBBB3BBsEdwV4ZNH1ClvDniOXCGh5oifNGTt6lv1XfsPXutTGyMWvh/038vtOb2xdY/L1fEx62ubrLLI3aaO1HY+tV8VqvwstbYg3Z5htUSK+XTv12WbKswjxEYlidqafmDQtpHQhbi8yYmJtL2YmJi8I9mFfrBM5LQQQ2gOp2J6ilvax3CuRQlhAAvzE2Qdzy35D05/+qWviMO5xJExaLugPRoqyeVi/iVvIgxxGmgF1kAAnv6q7WO4VyIMcgB/Krfoa+HuWvmEHFikj1Butpbqq6ttXVi/da3EQamWwCKJseoO0irA0jmTQFmgOVeiuwcQYwN1Anckja3EkudVmrJJWyiDQyrB8EOBk16nahsBWwG5slxNWST1WPLYJGPkL3NIkOrZxNHltY2GkAfqj1UmiCMzfDPfCY43bk7udIWGt7pzWO36cuq2MKx2hge4Bw9rQ6wfiQLHwC20QaGYYYytDdYa2/MNrIDga/YRXLfrVHBmuX6442Rua3huBGqzsGOaBe56j4A91LIg0sth4bA0kE28mq/Ke51bAd65DksOVZY2EvdrDi8k+y0UCbq9yfnXopNEEZhssayd82sHX+TpaK5X5vh6etpJljTiGz6wCLtulu/l0+0KPzv4KTRBEY7KRJOybiAaNPl03elxdzvbn2W7i49bXNDgLI5jUKFE7XvyW0iDUw2HDY2s1AaerAGDmdtO9Df8Ax5rHi8GHyNfqZ5S07sDj5S47Ovbn8FvogxgCydXPpew9R+z/AGTcfk+WiDX5w7Vp5NDfZBFnc2TzJ72pREEXl+WiKV8msHWKrSAfauyb3PrQV+PwfFMRtg4btQ1t1UdJbtuK2J+NdlIog5PxsfND7pP9Nc7an/Hp80Huk/01zKw1Tq5Hafmq/bpDOZArTIsayxRX7lTWWgrGCfRVWwAivurWcmFcFaCrguslsLlryx17lsBCLVZTd3/4Mf7I/wDTO/lYuuXJ/g0bWFf+md/KxdYvBzHFq5uqynBo5CIiwtgREQEREBERBgxOKbHWo0De5oAU0uJJPSgsYzOKyNY2APp5nOaBffU0iudrLicK2StXS63rmCP4FYm5ewO1C7u+exOtzwfgXu+fuQVfmMQBPEbttzHOif4A/I9kbj49LXFwGoXRI7gEe8Ege8rEMpjHLUKAaCHGw0BwDB+bTneu/oKDKYwQQXAtvTTvZuiSPfX7SgyNzGI7F7Qd9i5vIF41bHl5HH9U9iqT5iwRvkbcgZeoMLbFN1H2iN6rb1VkmVRkOFe0DdkkbmQ70Qecjuo5quHy+mSNe7VxSdXMc2NZQ37NCC9uYMunHQ660ucyyaZ9Un67R8R3F2uzSMPYy74gcQ4UWjS1rtze1hwI/wDV3vwDC4uo2TZ3PP8AF/8AjZ8lrR5LHp0vGonVdWB5ntdVXyGhjR6NpBfhM1EtaI5D3vQNHnc3e3c/KTQs16kA0gzdj43yBppjdRFxknYmqa40duTqWZuXtBtpc2ySacRqt7n0fi48u9cldBgg1pYHPqqHm9kD6pG4+5Bkws4e0OHI31aeRrm0kdO6yrFh4AxukXzJ35kuJc4/EklZUBERAREQEREBERBx/j32oPdJ/prml0vj324PdJ/prnoYr9yw1eJyO0/NV+3SFYo79y2wFQBVSIs0oiwiIpS5YhVDQrdSqHFdXLOu0IR6qiqFSR6F+Dj+yv8A0zv5WLqlyv4Of7M/9M7+Vi6peFmOLVzdXlOBRyERFhbAiIgIiIIR8M3He4BxaXDa3Aaai39ujuHbBo5nfoaYfGTSsmDSNQiaWlmk1IeJbQdRBAptX39VOJSCHInBNAlpJcL2Ip0dcj1Bea9PnjxGOmjIDi2yfLs232IttJddAueNr5D9acRBGsmn4biW04PA2A3Zbbc1t9LOx7flbXZxcQTVUCRZLRsNbACPNuS0vJ7ED9aVRBD8bFAN8rSSATtQDi0eWhflvVv7t+qz4ozB7tA20ki99RAFN3O1m91IogjsVJPxC1g8pDfNQ287Q7mdzpLiPdy74eNiQG23USGkkAAA/lMqz/vryBl0QQsJlihNghxfCBdONFkLH0L53r+I69bjiMTt+L6bnblftAX7VdL57dipchVQQ0b52ulOkkOLS07WfLE1xI301uaAPJ3oDhGY4iw2m8ShcY0+X8U1xNhxIOokbivZ7gun0QR2BlmLwJG+XSTY6HVtd8yW+7rsFIoiAiIgIiICIiDkfHLLfAPST+Mah2AclPeMvah90n+RQIVJjVye0vNV+3SF1KtKgKqqtEREQcEyQjkVIMOyIusltVLwqoixyo9C/Bx/Zn/pnfysXVIi8LMcWrm6rKcCjkIiLC2RERAREQEREBERAREQEREBERAREQEREBERAREQEREBERBy/jL2ofdJ/kUCFVFSXJ7S81X7dIFVqoiq0VyIiD//2Q==
language: php | Laravel
---

### 1. Menambahkan Depedency Tiny MCE
Di sini kita perlu menambahkan depedency Tiny MCE contoh dengan cdn pada layout pada berikut.
```html
<script src="https://cdn.tiny.cloud/1/API_KEY_HERE/tinymce/5/tinymce.min.js" referrerpolicy="origin">
```

### 2. Menambahkan Script Pada View
Pada langkah ini menambahkan script pada view untuk menampilkan text editor.

Selector yang akan di load.
```bash
<textarea class="form-control" id="body" name="body" ></textarea>
```

Kemudian tambahkan script.
```bash
<script>
    tinymce.init({
        selector: '#body',
        plugins: 'lists link image media code',
        toolbar: 'undo redo | styleselect | forecolor | bold italic | alignleft aligncenter alignright alignjustify | outdent indent | link image | code',
        file_picker_types: 'image',
        images_upload_handler: function (blobInfo, success, failure) {
            let data = new FormData();
            data.append('file', blobInfo.blob(), blobInfo.filename());
            data.append('_token', document.getElementsByName("_token")[0].value);
            axios.post("<?= url('admin/announcement/upload'); ?>", data).then(function (res) {
                success(res.data.location);
            }).catch(function (err) {
                failure('HTTP Error: ' + err.message);
            });
        },
        file_picker_callback: function(cb, value, meta) {
            var input = document.createElement('input');
            input.setAttribute('type', 'file');
            input.setAttribute('accept', 'image/*');
            input.onchange = function() {
                var file = this.files[0];
                var reader = new FileReader();
                reader.readAsDataURL(file);
                reader.onload = function () {
                    var id = 'blobid' + (new Date()).getTime();
                    var blobCache =  tinymce.activeEditor.editorUpload.blobCache;
                    var base64 = reader.result.split(',')[1];
                    var blobInfo = blobCache.create(id, file, base64);
                    blobCache.add(blobInfo);
                    cb(blobInfo.blobUri(), { title: file.name });
                };
            };
            input.click();
        }
    });
</script>
```

### 3. Membuat Fungsi Upload Pada Controller
Pada langkah ini kita akan membuat fungsi upload untuk menyimpan gambar pada storage.

Pada Route.
```bash
Route::post('file/upload', [FileController::class, 'upload'])->name('file.upload');
```

Pada Controller.
```bash
namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\Http\Controllers\Controller;
use Illuminate\Support\Facades\Storage;

class FileController extends Controller
{

    /**
    * Handle file upload and return location.
    *
    * @param  Illuminate\Http\Request  $request
    * @return \Illuminate\Http\Response
    */
    public function upload(Request $request)
    {
        $this->validate($request, [ 'file' => 'required|image' ]);
        
        $filename = $request->file->getClientOriginalName();
        $location = url('storage/upload-image/' . $filename);
        
        try {
            $request->file->storeAs('public/upload-image', $filename);
        } catch (Exception $e) {
            return abort(500, 'Invalid upload image.');
        }
        
        return response()->json([ 'location' => $location ]);
    }
}
```

### Catatan
Pada upload di storage jika kita gunakan default tanpa nama file bisa gunakan :
```bash
$location = $request->file->storePublicly('upload-image', 'public');
```

Sekian untuk kali ini semoga bermanfaat :D untuk lebih lanjut bisa kunjungi [link](https://kevinchoppin.dev/blog/implementing-simple-file-uploads-in-tinymce-editor) tersebut.
