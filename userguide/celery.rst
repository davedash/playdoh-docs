===========================
Asynchronous Tasks (Celery)
===========================


One goal in developing web projects is to minimize request times.
Long request times lead to users leaving your website and ultimately
a loss of revenue and mindshare.
Smaller request times lead to huger bags of money that you can take to the
bank.

If you can separate things that need to happen immediately
(e.g. sending a message, setting a privacy setting) versus things that can
take some time (e.g. deleting a tag, updating a search index)
you can take advantage of a queue.

Playdoh includes Celery for managing asynchronous task queues.
Celery is one of the more popular task queue systems for Django.

In production Celery uses RabbitMQ (or some other backend) to store tasks
that you want to do later.

While developing locally, Playdoh defaults to::

    CELERY_ALWAYS_EAGER = True

This causes your Celery tasks to happen during the request-response cycle,
which is great for development.

You can place your tasks in ``tasks.py`` and decorate them like so::

    from celery.task import task


    @task
    def my_awesome_task():
        time.sleep(100000)


You can get more advanced.


.. seealso::

    * `Django Celery Docs <http://readthedocs.org/docs/django-celery/>`_
    * `Queue everything and delight everyone
       <http://decafbad.com/blog/2008/07/04/queue-everything-and-delight-everyone>`_
    * `Example ``settings/local.py``
       <https://github.com/mozilla/affiliates/blob/master/settings/local.py-dist>`_
