0.3.2 (2019-07-21)
==================

- Fix exception during import when executing Python with ``-s`` and ``-S`` flags causing ``site.USER_SITE`` to be missing (`#114 <https://github.com/Delgan/loguru/issues/114>`_).


0.3.1 (2019-07-13)
==================

- Fix ``retention`` and ``rotation`` issues when file sink initiliazed with ``delay=True`` (`#113 <https://github.com/Delgan/loguru/issues/113>`_).
- Fix ``"sec"`` no longer recognized as a valid duration unit for file ``rotation`` and ``retention`` arguments.
- Ensure stack from the caller is displayed while formatting exception of a function decorated with ``@logger.catch`` when ``backtrace=False``.
- Modify datetime used to automatically rename conflicting file when rotating (it happens if file already exists because ``"{time}"`` not presents in filename) so it's based on the file creation time rather than the current time.


0.3.0 (2019-06-29)
==================

- Remove all dependencies previously needed by ``loguru`` (on Windows platform, it solely remains ``colorama`` and ``win32-setctime``).
- Add a new ``logger.patch()`` method which can be used to modify the record dict on-the-fly before it's being sent to the handlers.
- Modify behavior of sink option ``backtrace`` so it only extends the stacktrace upward, the display of variables values is now controlled with the new ``diagnose`` argument (`#49 <https://github.com/Delgan/loguru/issues/49>`_).
- Change behavior of ``rotation`` option in file sinks: it is now based on the file creation time rather than the current time, note that proper support may differ depending on your platform (`#58 <https://github.com/Delgan/loguru/issues/58>`_).
- Raise errors on unknowns color tags rather than silently ignoring them (`#57 <https://github.com/Delgan/loguru/issues/57>`_).
- Add the possibility to auto-close color tags by using ``</>`` (e.g. ``<yellow>message</>``).
- Add coloration of exception traceback even if ``diagnose`` and ``backtrace`` options are ``False``.
- Add a way to limit the depth of formatted exceptions traceback by setting the conventional ``sys.tracebacklimit`` variable (`#77 <https://github.com/Delgan/loguru/issues/77>`_).
- Add ``__repr__`` value to the ``logger`` for convenient debugging (`#84 <https://github.com/Delgan/loguru/issues/84>`_).
- Remove colors tags mixing directives (e.g. ``<red,blue>``) for simplification.
- Make the ``record["exception"]`` attribute unpackable as a ``(type, value, traceback)`` tuple.
- Fix error happening in some rare circumstances because ``frame.f_globals`` dict did not contain ``"__name__"`` key and hence prevented Loguru to retrieve the module's name. From now, ``record["name"]`` will be equal to ``None`` in such case (`#62 <https://github.com/Delgan/loguru/issues/62>`_).
- Fix logging methods not being serializable with ``pickle`` and hence raising exception while being passed to some ``multiprocessing`` functions (`#102 <https://github.com/Delgan/loguru/issues/102>`_).
- Fix exception stack trace not colorizing source code lines on Windows.
- Fix possible ``AttributeError`` while formatting exceptions within a ``celery`` task (`#52 <https://github.com/Delgan/loguru/issues/52>`_).
- Fix ``logger.catch`` decorator not working with generator and coroutine functions (`#75 <https://github.com/Delgan/loguru/issues/75>`_).
- Fix ``record["path"]`` case being normalized for no necessary reason (`#85 <https://github.com/Delgan/loguru/issues/85>`_).
- Fix some Windows terminal emulators (mintty) not correctly detected as supporting colors, causing ansi codes to be automatically stripped (`#104 <https://github.com/Delgan/loguru/issues/104>`_).
- Fix handler added with ``enqueue=True`` stopping working if exception was raised in sink although ``catch=True``.
- Fix thread-safety of ``enable()`` and ``disable()`` being called during logging.
- Use Tox to run tests (`#41 <https://github.com/Delgan/loguru/issues/41>`_).


0.2.5 (2019-01-20)
==================

- Modify behavior of sink option ``backtrace=False`` so it doesn't extend traceback upward automatically (`#30 <https://github.com/Delgan/loguru/issues/30>`_).
- Fix import error on some platforms using Python 3.5 with limited ``localtime()`` support (`#33 <https://github.com/Delgan/loguru/issues/33>`_).
- Fix incorrect time formatting of locale month using ``MMM`` and ``MMMM`` tokens (`#34 <https://github.com/Delgan/loguru/pull/34>`_, thanks `@nasyxx <https://github.com/nasyxx>`_).
- Fix race condition permitting writing on a stopped handler.


0.2.4 (2018-12-26)
==================

- Fix adding handler while logging which was not thread-safe (`#22 <https://github.com/Delgan/loguru/issues/22>`_).


0.2.3 (2018-12-16)
==================

- Add support for PyPy.
- Add support for Python 3.5.
- Fix incompatibility with ``awscli`` by downgrading required ``colorama`` dependency version (`#12 <https://github.com/Delgan/loguru/issues/12>`_).


0.2.2 (2018-12-12)
==================

- Deprecate ``logger.start()`` and ``logger.stop()`` methods in favor of ``logger.add()`` and ``logger.remove()`` (`#3 <https://github.com/Delgan/loguru/issues/3>`_).
- Fix ignored formatting while using ``logging.Handler`` sinks (`#4 <https://github.com/Delgan/loguru/issues/4>`_).
- Fix impossibility to set empty environment variable color on Windows (`#7 <https://github.com/Delgan/loguru/issues/7>`_).


0.2.1 (2018-12-08)
==================

- Fix typo preventing README to be correctly displayed on PyPI.


0.2.0 (2018-12-08)
==================

- Remove the ``parser`` and refactor it into the ``logger.parse()`` method.
- Remove the ``notifier`` and its dependencies (``pip install notifiers`` should be used instead).


0.1.0 (2018-12-07)
==================

- Add logger.
- Add notifier.
- Add parser.


0.0.1 (2017-09-04)
==================

Initial release.
