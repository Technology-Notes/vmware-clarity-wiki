Hierarchical datagrids have heavy usability and performance concerns.
Expandable rows are good at keeping context of the content between rows and showing some additional data to support it.
When loading an entire new datatable or a page's worth of content inside of an expandable row, 
the user loses context of the datagrid which they are in.

Because of this, we recommend using a master-detail pattern, or ideally navigating to a dedicated details page for
a particular row.
