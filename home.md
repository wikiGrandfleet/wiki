<!-- TITLE: Installation Details -->
<!-- SUBTITLE: Python script for japanese games and content -->

# Wiki.js
## Markdown

| Test | Cool |
| ---  |   --- |
| Test|  Test |

Wiki, js supports standard markdown however the ability to include a folder of images is quite useful.

![Composer Arch](/uploads/engr-446/composer-arch.png "Composer Arch")

### Example Code

> Since markdown just renders html, pdf files can be embeeded using

```sh
<object data="https://github.com/FriendlyUser/ENGRCoopReportTemplate/blob/AuxReports/reportContent.pdf" type="application/pdf" width="700px" height="700px">
    <embed src="https://github.com/FriendlyUser/ENGRCoopReportTemplate/blob/AuxReports/reportContent.pdf">
        This browser does not support PDFs. Please download the PDF to view it: <a href="https://github.com/FriendlyUser/ENGRCoopReportTemplate/blob/AuxReports/reportContent.pdf">Download PDF</a>
    </embed>
</object>
```

##### Python Script

Hopefully you show up in the wiki, no errors are appearing

```python
# This scripts allows to get a list of all installed products in a windows
# machine. The code uses ctypes becuase there were a number of issues when
# trying to achieve the same win win32com.client
from collections import namedtuple
from ctypes import byref, create_unicode_buffer, windll
from ctypes.wintypes import DWORD
from itertools import count
 
# defined at http://msdn.microsoft.com/en-us/library/aa370101(v=VS.85).aspx
UID_BUFFER_SIZE = 39
PROPERTY_BUFFER_SIZE = 256 
ERROR_MORE_DATA = 234
ERROR_INVALID_PARAMETER = 87
ERROR_SUCCESS = 0
ERROR_NO_MORE_ITEMS = 259 
ERROR_UNKNOWN_PRODUCT = 1605 
 
# diff propoerties of a product, not all products have all properties
PRODUCT_PROPERTIES = [u'Language',
                      u'ProductName',
                      u'PackageCode',
                      u'Transforms',
                      u'AssignmentType',
                      u'PackageName',
                      u'InstalledProductName',
                      u'VersionString',
                      u'RegCompany',
                      u'RegOwner',
                      u'ProductID',
                      u'ProductIcon',
                      u'InstallLocation',
                      u'InstallSource',
                      u'InstallDate',
                      u'Publisher',
                      u'LocalPackage',
                      u'HelpLink',
                      u'HelpTelephone',
                      u'URLInfoAbout',
                      u'URLUpdateInfo',] 
 
# class to be used for python users :)
Product = namedtuple('Product', PRODUCT_PROPERTIES)
 
 
def get_property_for_product(product, property, buf_size=PROPERTY_BUFFER_SIZE):
    """Retruns the value of a fiven property from a product."""
    property_buffer = create_unicode_buffer(buf_size)
    size = DWORD(buf_size)
    result = windll.msi.MsiGetProductInfoW(product, property, property_buffer,
                                           byref(size))
    if result == ERROR_MORE_DATA:
        return get_property_for_product(product, property,
                2 * buf_size)
    elif result == ERROR_SUCCESS:
        return property_buffer.value
    else:
        return None
 
 
def populate_product(uid):
    """Return a Product with the different present data."""
    properties = []
    for property in PRODUCT_PROPERTIES:
        properties.append(get_property_for_product(uid, property))
    return Product(*properties) 
 
 
def get_installed_products_uids():
    """Returns a list with all the different uid of the installed apps."""
    # enum will return an error code according to the result of the app
    products = []
    for i in count(0):
        uid_buffer = create_unicode_buffer(UID_BUFFER_SIZE)
        result = windll.msi.MsiEnumProductsW(i, uid_buffer)
        if result == ERROR_NO_MORE_ITEMS:
            # done interating over the collection
            break
        products.append(uid_buffer.value)
    return products
 
 
def get_installed_products():
    """Returns a collection of products that are installed in the system."""
    products = []
    for puid in  get_installed_products_uids():
        products.append(populate_product(puid))
    return products 
 
 
def is_product_installed_uid(uid):
    """Return if a product with the given id is installed.
 
    uid Most be a unicode object with the uid of the product using
    the following format {uid}
    """
    # we try to get the VersisonString for the uid, if we get an error it means
    # that the product is not installed in the system.
    buf_size = 256
    uid_buffer = create_unicode_buffer(uid)
    property = u'VersionString'
    property_buffer = create_unicode_buffer(buf_size)
    size = DWORD(buf_size)
    result = windll.msi.MsiGetProductInfoW(uid_buffer, property, property_buffer,
                                           byref(size))
    if result == ERROR_UNKNOWN_PRODUCT:
        return False
    else:
        return True

# consider adding this table to my dashboard
apps=get_installed_products()
for app in apps:
    try:
        print(app.InstalledProductName)
    except:
        print('Unicode Installed package')
        print(app.InstalledProductName.encode('utf-8'))
```

###### Test 
