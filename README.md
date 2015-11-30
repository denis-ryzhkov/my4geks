my4geks
=======

[MySQL][] for [Gevent][] kept [Simple][].
[MySQL]: https://www.mysql.com/
[Gevent]: http://www.gevent.org/
[Simple]: https://en.wikipedia.org/wiki/KISS_principle

Usage:

    # pip install my4geks
    import gevent.monkey ; gevent.monkey.patch_all()
    from my4geks import db, db_config, db_transaction

    db_config.update(user='user', password='password', database='test')
        # Defaults: host='127.0.0.1', port=3306, pool_size=10.

    def on_request(): # Inside a greenlet:
        item = db('SELECT * FROM `items` WHERE `id` = %s', item_id).row

        for item in db('SELECT `id`, `name` FROM `items` WHERE `name` IN %s, [value1, value2]).rows:
            print('{}\t{}'.format(item.id, item.name))

        def code():
            db('INSERT INTO `table1` (`quantity`) VALUES (%s)', -100)
            db('INSERT INTO `table2` (`quantity`) VALUES (%s)', +1/0)
        db_transaction(code)

my4geks version 0.1.1  
Copyright (C) 2015 by Denis Ryzhkov <denisr@denisr.com>  
MIT License, see http://opensource.org/licenses/MIT
