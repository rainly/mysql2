# Changelog

## 0.1.9 (July 17th, 2010)
* Support async ActiveRecord access with fibers and EventMachine (mperham)
* string encoding support for 1.9, respecting Encoding.default_internal
* added support for rake-compiler (tenderlove)
* bugfixes for ActiveRecord driver
** one minor bugfix for TimeZone support
** fix the select_rows method to return what it should according to the docs (r-stu31)
* Mysql2::Client#fields method added - returns the array of field names from a resultset, as strings
* Sequel adapter
** bugfix regarding sybolized field names (Eric Wong)
** fix query logging in Sequel adapter
* Lots of nice code cleanup (tenderlove)
** Mysql2::Error definition moved to pure-Ruby
** Mysql2::client#initialize definition moved to pure-Ruby
** Mysql2::Result partially moved to pure-Ruby

## 0.1.8 (June 2nd, 2010)
* fixes for AR adapter for timezone juggling
* fixes to be able to run benchmarks and specs under 1.9.2

## 0.1.7 (May 22nd, 2010)
* fix a bug when using the disconnect! method on a closed connection in the AR driver

## 0.1.6 (May 14th, 2010)
* more fixes to the AR adapter related to casting
* add missing index creation override method to AR adapter
* added sql_state and error_number methods to the Mysql2::Error exception class

## 0.1.5 (May 12th, 2010)
* quite a few patches from Eric Wong related to thread-safety, non-blocking I/O and general cleanup
** wrap mysql_real_connect with rb_thread_blocking_region
** release GVL for possibly blocking mysql_* library calls
** [cleanup] quiet down warnings
** [cleanup] make all C symbols static
** add Mysql2::Client#close method
** correctly free the wrapped result in case of EOF
** Fix memory leak from the result wrapper struct itself
** make Mysql2::Client destructor safely non-blocking
* bug fixes for ActiveRecord adapter
** added casting for default values since they all come back from Mysql as strings (!?!)
** missing constant was added
** fixed a typo in the show_variable method
* switched over sscanf for date/time parsing in C
* made some specs a little finer-grained
* initial Sequel adapter added
* updated query benchmarks to reflect the difference between casting in C and in Ruby

## 0.1.4 (April 23rd, 2010)
* optimization: implemented a local cache for rows that are lazily created in ruby during iteration. The MySQL C result is freed as soon as all the results have been cached
* optimization: implemented a local cache for field names so every row reuses the same objects as field names/keys
* refactor the Mysql2 connection adapter for ActiveRecord to not extend the Mysql adapter - now being a free-standing connection adapter

## 0.1.3 (April 15th, 2010)
* added an EventMachine Deferrable API
* added an ActiveRecord connection adapter
** should be compatible with 2.3.5 and 3.0 (including Arel)

## 0.1.2 (April 9th, 2010)
* fix a bug (copy/paste fail) around checking for empty TIME values and returning nil (thanks @marius)

## 0.1.1 (April 6th, 2010)
* added affected_rows method (mysql_affected_rows)
* added last_id method (last_insert_id)
* enable reconnect option by default
* added initial async query support
* updated extconf (thanks to the mysqlplus project) for easier gem building

## 0.1.0 (April 6th, 2010)
* initial release