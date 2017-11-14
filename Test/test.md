Drupal Unit Test Suite: 自动检测测试文件
core/phpunit.xml.dist文件定义了测试文件的检测位置
  core/tests/
  core/modules/*/tests
  modules
  sites/*/modules

排除:
  <exclude> ... </exclude>

核心类:
  文件夹: core/tests/Drupal/Tests/Core/  后斜线
  命名空间: \Drupal\Tests\Core  前斜线

运行所有的PHPUnit测试:
  cd core
  ./vendor/phpunit/phpunit/phpunit

运行选择的PHPUnit测试:
  ./vendor/phpunit/phpunit/phpunit --list-groups

运行一个指定的PHPUnit测试组:
  ./vendor/phpunit/phpunit/phpunit --group Groupname

运行多个指定的PHPUnit测试组:
  ./vendor/phpunit/phpunit/phpunit --group Groupname1,Groupname2
  
排除运行指定的PHPUnit测试组:
  ./vendor/phpunit/phpunit/phpunit --exclude-group Groupname

运行指定的测试方法
  ./vendor/phpunit/phpunit/phpunit --filter=MyMethodTest

产生一个代码测试报告:
  ./vendor/phpunit/phpunit/phpunit --coverage-html /tmp/report


使用自动测试命令测试PHPUnit用例
  前提是启用Testing模块

  php core/scripts/run-tests.sh PHPUnit
