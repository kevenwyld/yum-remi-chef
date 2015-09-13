yum-remi Cookbook
=================
[![Build Status](https://travis-ci.org/chef-cookbooks/yum-remi.svg?branch=master)](http://travis-ci.org/chef-cookbooks/yum-epel)
[![Cookbook Version](https://img.shields.io/cookbook/v/yum-remi.svg)](https://supermarket.chef.io/cookbooks/yum-epel)

The yum-remi cookbook takes over management of the repositoryids of
the [remi](http://rpms.famillecollet.com/) repository . It allows
attribute manipulation of `remi`, `remi-php55`, `remi-php56`, and
`remi-test` repositories.

Requirements
------------
#### Chef
* Chef 11+

#### Cookbooks
* yum version 3.0.0 or higher

#### Platforms
The following platforms have been tested with Test Kitchen:

```
|-----------+------+------------+------------|
|           | remi | remi-php55 | remi-php56 |
|-----------+------+------------+------------|
| centos-5  | X    | X          | X          |
|-----------+------+------------+------------|
| centos-6  | X    | X          | X          |
|-----------+------+------------+------------|
| centos-7  | X    | X          | X          |
|-----------+------+------------+------------|
| redhat-7  | X    | X          | X          |
|-----------+------+------------+------------|
| fedora-20 | X    |            | X          |
|-----------+------+------------+------------|
| fedora-21 | X    |            |            |
|-----------+------+------------+------------|
```

Amazon Linux is *not* supported by the Remi repository. Amazon
maintains their own PHP packages natively, as php53, php54, php55, and
php56.

Attributes
----------
The following attributes are set by default

``` ruby
default['yum']['remi']['repositoryid'] = 'remi'
default['yum']['remi']['baseurl'] = 'http://rpms.famillecollet.com/enterprise/5/remi/$basearch/'
default['yum']['remi']['description'] = 'Les RPM de remi pour Enterprise Linux 5 - $basearch'
default['yum']['remi']['enabled'] = true
default['yum']['remi']['gpgcheck'] = true
default['yum']['remi']['gpgkey'] = 'http://rpms.famillecollet.com/RPM-GPG-KEY-remi'
```

``` ruby
default['yum']['remi-php55']['repositoryid'] = 'remi-php55'
default['yum']['remi-php55']['baseurl'] = 'http://rpms.famillecollet.com/enterprise/5/php55/$basearch/'
default['yum']['remi-php55']['description'] = 'Les RPM de remi de PHP 5.5 pour Enterprise Linux 5 - $basearch'
default['yum']['remi-php55']['enabled'] = true
default['yum']['remi-php55']['gpgcheck'] = true
default['yum']['remi-php55']['gpgkey'] = 'http://rpms.famillecollet.com/RPM-GPG-KEY-remi'
```

``` ruby
default['yum']['remi-php55']['repositoryid'] = 'remi-php56'
default['yum']['remi-php55']['baseurl'] = 'http://rpms.famillecollet.com/enterprise/5/php56/$basearch/'
default['yum']['remi-php55']['description'] = 'Les RPM de remi de PHP 5.6 pour Enterprise Linux 5 - $basearch'
default['yum']['remi-php55']['enabled'] = true
default['yum']['remi-php55']['gpgcheck'] = true
default['yum']['remi-php55']['gpgkey'] = 'http://rpms.famillecollet.com/RPM-GPG-KEY-remi'
```

Recipes
-------
* default - Walks through node attributes and feeds a yum_resource
  parameters. The following is an example a resource generated by the
  recipe during compilation.

```ruby
  yum_repository 'remi' do
    baseurl 'http://rpms.famillecollet.com/enterprise/6/remi/$basearch/'
    description 'Les RPM de remi pour Enterprise Linux 6 - $basearch'
    enabled true
    gpgcheck true
    gpgkey 'http://rpms.famillecollet.com/RPM-GPG-KEY-remi'
  end
```

Usage Example
-------------
To disable the remi repository through a Role or Environment definition

```
default_attributes(
  :yum => {
    :remi => {
      :enabled => {
        false
       }
     }
   }
 )
```

More Examples
-------------
Point the base and updates repositories at an internally hosted server.

```
node.default['yum']['remi']['enabled'] = true
node.default['yum']['remi']['mirrorlist'] = nil
node.default['yum']['remi']['baseurl'] = 'https://internal.example.com/enterprise/5/remi/$basearch/'
node.default['yum']['remi']['sslverify'] = false

include_recipe 'yum-remi'
```

License & Authors
-----------------

**Author:** Cookbook Engineering Team (<cookbooks@chef.io>)

**Copyright:** 2015, Chef Software, Inc.
```
Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
