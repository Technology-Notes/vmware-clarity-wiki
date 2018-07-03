Non-paginated datagrids in Clarity have a minimum height of 2 rows. There are two reasons for this.
The first one is simply to keep it harmonious, maintain a separation between the header and the footer.
The second is that many real-life use cases involve displaying an empty datagrid with a spinner while the data
is being loaded. Given our current design for said spinner, we need the datagrid to be at least 2 rows high
to display it correctly.