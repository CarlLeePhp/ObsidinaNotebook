- [x] Confirm before delete anything.
- [ ] Sale react page


#### Confirm Delete
A component was built for it.
```html
<ConfirmDelete
        isDelete={isDelete}
        message={deleteMessage}
        setDeleteConfirmOpen={setDeleteConfirmOpen}
        confirmDelete={deleteSale}
      />
```

We need these state from its parent:
isDelete, deleteMessage
We also need these methods from its parent:
setDeleteConfirmOpen, confirmDelete