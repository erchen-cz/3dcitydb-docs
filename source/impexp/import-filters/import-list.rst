.. _impexp_import_list_filter:

Import list filter
------------------

The import list filter allows you to provide a list of city objects that shall be
imported or skipped during import.

.. figure:: /media/impexp_import_list_filter.png
   :name: impexp_import_list_filter_fig
   :align: center

   Import list filter for import operations.

Import lists are simple comma-separated values (CSV) files that contain the
identifiers of the city objects to be imported or skipped. Each identifier
must be put on a separate line (row) of the file, and each line may contain additional
values (columns) separated by a delimiter (typically a single reserved character such
as comma, semicolon, tab, etc.). The first record may be reserved as header containing
a list of column names. Usually, every row has the same sequence of columns. If a line
starts with a predefined comment marker (typically a single reserved character
such as ``#``), the entire row is ignored and skipped.

Due to their simple structure, import lists can be easily created with external
tools and processes. The following snippet shows an example of a simple import list
that can be used with this import filter. It just provides an identifier per row.
The first line is used as header.

.. code-block:: bash
   :linenos:

   GMLID
   ID_0815
   ID_0816
   ID_0817
   ID_0818
   ...

To use an import list, simply provide the full path to the CSV file. The further input fields of
the dialog define the structure and content of the CSV file so that the identifiers
can be correctly parsed from the file and used in the import operation. For this
purpose, you can specify the delimiter used for separating values in the import list
(by default, a comma is assumed as delimiter). If the values in the import list are
quoted, you can also define the character used as quote (typically double quotes
are used). And the character used as comment marker as well as the encoding of
the import list can be specified.

Use the *Preview* button to get a preview of the first few lines of the import list
when applying the provided options for parsing and interpreting the import list.
This preview shows the contents of the import list in tabular form and is printed
to the console window. It is very helpful to adapt and specify the delimiter
character(s), quoting rules and comment marker. The preview should only show
the lines containing identifiers, but no header line or comments.
To identify the column which holds the identifiers in the file, you can either type
in the *Column name* in case the import list uses a header. Alternatively, you can
simply provide the *Column index* (note that the first column of a row has the
index 1). In the latter case, you can also specify whether the first record in the
CSV file shall be skipped because it is a header line.

Finally, define the mode of the import list filter. You can either choose to
*only import objects from the list* or to *skip objects from the list* instead.
During import, the identifiers from the import list are matched against the identifiers
of the city objects in the input file. Based on the defined filter mode, matching
objects are either imported or skipped.

.. note::
  You can also use the attribute filter (see :numref:`impexp_import_attribute_filter`)
  to provide a list of identifiers of city objects to be imported. However, the
  list of identifiers must be entered manually using the attribute filter, whereas
  import lists can be generated by software.

**Example use case**

One use case for this filter is when using import logs for the import operation
(see :numref:`impexp_import_preferences_import_log`).
Assume you start an import operation on a set of input files and the import is aborted or fails after
a certain amount of features. The import log will contain the identifiers of those city
objects that were successfully imported before the operation aborted. Thus, with this filter,
you can easily resume the import after having fixed the issues that caused the failure.
Since the import log is a CSV file, you can simply use it as import list and set the
filter mode to *skip objects from the list*. When starting the import operation with
these settings again, only those city objects will be imported from the input files that
have not been processed in the first run.