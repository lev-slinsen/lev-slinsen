# Django

```python
# Get default User model
from django.contrib.auth import get_user_model
User = get_user_model()
```

Getting a list of files as a single zip
```python
    @property
    def files_count(self):
        return self.files.all().count()

    def files_make_archive(self):
        files = self.files.all()

        # Makes a list of related file addresses
        filepaths = list(str(file.file) for file in files)
        # and an archive name in file system
        zip_filename = f"{self.title}.zip"

        # Creates a zip file in RAM to attach to the response
        response = HttpResponse(content_type='application/zip')
        zip_file = ZipFile(response, mode='w')

        # Storing each file in the zip
        for fpath in filepaths:
            # zip_file.write(f'{MEDIA_ROOT}/{fpath}')
            fdir, fname = os.path.split(fpath)
            zip_file.write(f'{MEDIA_ROOT}/{fpath}', f'/{zip_filename}/{fname}')

        # Sending zip back to the user
        response['Content-Disposition'] = 'attachment; filename={}'.format(zip_filename)
        return response
```
