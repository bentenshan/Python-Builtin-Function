property
=========

  ``function:: property([fget[, fset[, fdel[, doc]]]])``

   Return a property attribute for :term:`new-style class`\es (classes that
   derive from :class:`object`).

   *fget* is a function for getting an attribute value, likewise *fset* is a
   function for setting, and *fdel* a function for del'ing, an attribute.  Typical
   use is to define a managed attribute ``x``::

      class C(object):
          def __init__(self):
              self._x = None

          def getx(self):
              return self._x
          def setx(self, value):
              self._x = value
          def delx(self):
              del self._x
          x = property(getx, setx, delx, "I'm the 'x' property.")

   If then *c* is an instance of *C*, ``c.x`` will invoke the getter,
   ``c.x = value`` will invoke the setter and ``del c.x`` the deleter.

   If given, *doc* will be the docstring of the property attribute. Otherwise, the
   property will copy *fget*'s docstring (if it exists).  This makes it possible to
   create read-only properties easily using :func:`property` as a :term:`decorator`::

      class Parrot(object):
          def __init__(self):
              self._voltage = 100000

          @property
          def voltage(self):
              """Get the current voltage."""
              return self._voltage

   turns the :meth:`voltage` method into a "getter" for a read-only attribute
   with the same name.

   A property object has :attr:`getter`, :attr:`setter`, and :attr:`deleter`
   methods usable as decorators that create a copy of the property with the
   corresponding accessor function set to the decorated function.  This is
   best explained with an example::

      class C(object):
          def __init__(self):
              self._x = None

          @property
          def x(self):
              """I'm the 'x' property."""
              return self._x

          @x.setter
          def x(self, value):
              self._x = value

          @x.deleter
          def x(self):
              del self._x

   This code is exactly equivalent to the first example.  Be sure to give the
   additional functions the same name as the original property (``x`` in this
   case.)

   The returned property also has the attributes ``fget``, ``fset``, and
   ``fdel`` corresponding to the constructor arguments.

      versionadded:: 2.2

      versionchanged:: 2.5
      Use *fget*'s docstring if no *doc* given.

   .. versionchanged:: 2.6
      The ``getter``, ``setter``, and ``deleter`` attributes were added.

