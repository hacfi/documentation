## Install Feature Core

### Prerequisites

Please overview and install the necessary features before beginning the integration step.

| Name | Version |
| --- | --- |
| Cms | master |
| Product lists | master |
| Catalog | master |
| Customer | master |

### 1) Install the Required Modules Using Composer

Run the following command to install the required modules:
```Bash
composer require spryker/customer-catalog:"^1.0.0" --update-with-dependencies
```
:::(Warning) (Verification)
Make sure that the following modules were installed:

| Module | Expected Directory |
| --- | --- |
| CustomerCatalog | vendor/spryker/customer-catalog |
:::

## Set up Behavior

#### Configure the Catalog Search Count Query

Add the following plugins to your project:

| Plugin | Specification | Prerequisites | Namespace |
| --- | --- | --- | --- |
|  `ProductListQueryExpanderPlugin` | Extends a search query by filtering down results to match the current customer's product restrictions. | None |  `\Spryker\Client\CustomerCatalog\Plugin\Search\ProductListQueryExpanderPlugin` |

**src/Pyz/Client/Catalog/CatalogDependencyProvider.php**
    
 ```php
 <?php

namespace Pyz\Client\Catalog;

use Spryker\Client\Catalog\CatalogDependencyProvider as SprykerCatalogDependencyProvider;
use Spryker\Client\CustomerCatalog\Plugin\Search\ProductListQueryExpanderPlugin;

class CatalogDependencyProvider extends SprykerCatalogDependencyProvider
{
        /**
        * @return \Spryker\Client\Search\Dependency\Plugin\QueryExpanderPluginInterface[]
        */
         protected function createCatalogSearchCountQueryExpanderPlugins():             array
                    {
                             return [
                                        new ProductListQueryExpanderPlugin(),
                             ];
                 }
}
 ```

@(Warning)(Verification)(Make sure that the number of products on the catalog tab item is correct according to the customer's assigned product lists.)