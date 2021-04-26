# Storage Service

**Storage Service** is a Django + DRF package that help to work with model. 
Main advantage of this class is to provide **bulk** operations over the model data 
and upsert for single object with M2M relations. 

## Installation

Use the package manager [pip](https://pip.pypa.io/en/stable/) to install storage-service.

```bash
pip install storage_service
```

## Usage

```python
from storage_service.storage import StorageService

from blogs.helpers import BlogHelper  # optional
from blogs.serializers import BlogSerializer  # drf package


class BlogService(StorageService):
    def __init__(self):
        super().__init__()

        self.helper = BlogHelper  # optional

        self.model = BlogSerializer.Meta.model

        self.create_serializer_class = BlogSerializer
        self.get_serializer_class = BlogSerializer

        self.unique_identifier: str = 'pk'  # required unique model field
        self.unique_identifiers: list = []  # in case when you need more unique model fiedls
```

## Methods
`def serialize(self, entities, many=False):` - helps deserialize list of objects to dict.

`def get_next_id(self):` - returns next model primary key.


`def get_by(self, key: str = '', value=None, serialize=True):` - helps to retrieve 
model data by provided **key** & **value** parameters. If **serialize** is set to `True` then 
method will return deserialized  model data. Otherwise will be returned object.

- get_by, get_pk
- delete_by
- set_identifiers
- indexed
- upsert
- bulk_upsert
- bulk_delete
- bulk_get_or_create



## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[MIT](https://choosealicense.com/licenses/mit/)