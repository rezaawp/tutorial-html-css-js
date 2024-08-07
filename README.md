# tutorial-html-css-js

## js

### selector untuk trigger event di masing masing tag dengan membawa data
```javascript
$("button[title=\"Delete\"]").click(function() {
    let _this = $(this);
    Swal.fire({
        title: 'Are you sure?',
        text: "You won't be able to revert this!",
        icon: 'warning',
        showCancelButton: true,
        confirmButtonColor: '#3085d6',
        cancelButtonColor: '#d33',
        confirmButtonText: 'Yes, delete it!'
    }).then((result) => {
        if (result.isConfirmed) {
            Livewire.emit('delete', _this.data("delete-id"));
        }
    });
});
```

### validasi unique option di dalam select

### livewire event

### websocket pusher config

## Jquery

### Form submit ajax (Tanpa reload halaman)
#### HTML
```
<form id="user-store" action="{{ route('admin.users.store') }}" method="post" style="display: contents" enctype="multipart/form-data">
@csrf
<div class="modal-body">
    <div class="mb-3">
        <label for="name">Name</label>
        <input type="text" class="form-control" name="name" required autocomplete="off">
    </div>
    ... Input tags ...
</div>
<div class="modal-footer">
    <button type="button" class="btn btn-label-secondary" data-bs-dismiss="modal">
        Close
    </button>
    <button type="submit" class="btn btn-primary">Submit</button>
</div>
</form>
```

#### JQuery
```js
$("#user-store").submit(function(e) {
e.preventDefault()
    helpers.ajax({
        url: $(this).attr('action'),
        data: $(this).serialize(),
        addons_success: function() {
            dbs.ajax.reload()
            $("#user-store")[0].reset()
            $("#modal-add").modal('hide')
        }
    })
})
```

#### helpers.ajax
```js
ajax({
    url,
    data,
    type = 'POST',
    success,
    error,
    cache,
    processData = true,
    contentType,
    addons_success = () => { },
    addons_error = () => { },
    beforeSend,
    addons_beforeSend = () => { },
}) {
    $.ajax({
        url: url,
        type: type,
        headers: {
            'X-CSRF-TOKEN': $('meta[name="csrf-token"]').attr('content')
        },
        cache: cache ?? true,
        processData: processData,
        contentType: contentType ? contentType : 'application/x-www-form-urlencoded; charset=UTF-8',
        data: data,
        beforeSend: function () {
            if (typeof beforeSend == 'function') {
                beforeSend()
            } else {
                Swal.fire({
                    html: '<div class="d-flex justify-content-center"><div class="sk-grid sk-secondary"><div class="sk-grid-cube"></div><div class="sk-grid-cube"></div><div class="sk-grid-cube"></div><div class="sk-grid-cube"></div><div class="sk-grid-cube"></div><div class="sk-grid-cube"></div><div class="sk-grid-cube"></div><div class="sk-grid-cube"></div><div class="sk-grid-cube"></div></div></div><br>Please wait a moment...',
                    allowOutsideClick: false,
                    buttonsStyling: false,
                    showConfirmButton: false,
                });
                addons_beforeSend();
            }
        },
        success: function (res) {
            if (typeof success == 'function') {
                success(res)
            } else {
                let swal = Swal.fire({
                    icon: 'success',
                    text: res.message,
                    customClass: {
                        confirmButton: 'btn btn-primary'
                    },
                    buttonsStyling: false,
                    timer: 1200,
                });
                addons_success({ res, swal });
            }
        },
        error: function (res) {
            if (typeof error == 'function') {
                error(data)
            } else {
                if (res.responseJSON) {
                    Swal.fire({
                        icon: 'error',
                        text: res.responseJSON.message,
                        showClass: {
                            popup: 'animate__animated animate__shakeX'
                        },
                        customClass: {
                            confirmButton: 'btn btn-primary'
                        },
                        buttonsStyling: false
                    })
                } else {
                    Swal.fire({
                        icon: 'error',
                        text: 'Something went wrong!',
                        showClass: {
                            popup: 'animate__animated animate__shakeX'
                        },
                        customClass: {
                            confirmButton: 'btn btn-primary'
                        },
                        buttonsStyling: false
                    })
                }
                addons_error(res);
            }
        }
    });
}
```

