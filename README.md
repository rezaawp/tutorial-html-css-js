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

