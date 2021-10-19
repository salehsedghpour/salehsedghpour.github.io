---
title: Service Mesh
layout: page
permalink: /research/service-mesh
dataTable: true


---
<h1>Service Mesh</h1>
<script>
$(document).ready(function() {
    $('#table').DataTable( {
        initComplete: function () {
            this.api().columns().every( function () {
                var column = this;
                var select = $('<select style="width: 100%"><option value=""></option></select>')
                    .appendTo( $(column.footer()).empty() )
                    .on( 'change', function () {
                        var val = $.fn.dataTable.util.escapeRegex(
                            $(this).val()
                        );
 
                        column
                            .search( val ? '^'+val+'$' : '', true, false )
                            .draw();
                    } );
 
                column.data().unique().sort().each( function ( d, j ) {
                    select.append( '<option value="'+d+'">'+d+'</option>' )
                } );
            } );
	    this.api().columns.adjust().draw();
        }
    } );
} );
</script>
<div style="width: 100%;">
<table id="table" class="display" style="width: 100%; table-layout: fixed" >
        <thead>
            <tr>
                <th>Title</th>
                <th>Authors</th>
                <th>Year</th>
                <th>Published in</th>
		<th>Tags </th>
		<th>Link</th>
            </tr>
        </thead>
        <tbody>
	{% for paper in site.data.service_mesh %}
		<tr>
		   <td>{{ paper.title }}</td>
		   <td>{{ paper.authors }}</td>
		   <td>{{ paper.year }}</td>
		   <td>{{ paper.publisher }}</td>
		   <td>{{ paper.tags }}</td>
		   <td><a href="{{ paper.link }}" target="_blank">Download</a></td>
		</tr>
	{% endfor %}
        </tbody>
	<tfoot>
		<tr>
                <th>Title</th>
                <th>Authors</th>
                <th>Year</th>
                <th>Published in</th>
                <th>Tags </th>
                <th>Link</th>
            </tr>
	</tfoot>
    </table>
</div>
