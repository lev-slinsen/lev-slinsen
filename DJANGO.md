# Django

```python
# Get default User model
from django.contrib.auth import get_user_model
User = get_user_model()
```

```python
# Get now with django lib
from django.utils import timezone
now = timezone.now()
```
### Models
Utility for created and updated fields
```python
from django.db import models

class CreatedUpdated(models.Model):
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
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
### Testing

Class based:
```python
from django.urls import reverse
from rest_framework.test import APITestCase

from ...models import Statement, StatementType, Service


class ApiTest(APITestCase):

    def setUp(self):

        # URLs
        #
        self.accept_statement = reverse('api:accept_statement')

        # Users
        #
        self.user_admin = User.objects.create(username='admin', is_superuser=True)
        self.user_1 = User.objects.create(username='user_1')

        # Objects
        #
        self.service = Service.objects.create(position=1)
        self.statement_type = StatementType.objects.create(position=1, service_id=self.service.id)
        self.statement = Statement.objects.create(statement_type_id=self.statement_type.id, user=self.user_1)

    def tearDown(self):
        return super().tearDown()


class TestAcceptStatement(ApiTest):

    def test__accept_statement__login_required(self):
        res = self.client.get(self.accept_statement)

        self.assertEqual(res.status_code, 401)
        self.assertEqual(res.data, {'error': {'message': 'login required'}})

    def test__accept_statement__id_required(self):
        self.client.force_login(self.user_admin)
        res = self.client.post(self.accept_statement)

        self.assertEqual(res.status_code, 400)
        self.assertEqual(res.data, {'error': {'message': 'id required'}})

    def test__accept_statement__doesnt_exist(self):
        self.client.force_login(self.user_admin)
        data = {
            'id': self.statement.id + 12
        }
        res = self.client.post(self.accept_statement, data, format='json')

        self.assertEqual(res.status_code, 400)
        self.assertEqual(res.data, {'error': {'message': 'no object with this id'}})

    def test__accept_statement__validate_owner(self):
        self.client.force_login(self.user_admin)
        data = {
            'id': self.statement.id
        }
        res = self.client.post(self.accept_statement, data, format='json')

        self.assertEqual(res.status_code, 400)
        self.assertEqual(res.data, {'error': {'message': 'object does not belong to the user'}})
```
___
Method based:
```python
@pytest.fixture(autouse=True)
def api_test(db):
    # Setup
    user_1 = User.objects.create(username="username", password="1234qwer")

    # # # #
    yield  #
    # # # #

    # Breakdown
    assert True


def test(db):
    # breakpoint()
    assert True
```
