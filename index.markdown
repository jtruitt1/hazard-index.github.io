---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
---

<table id="hazard-data" data-order='[[ 2, "asc" ]]'>
  {% for row in site.data.allHazard_thru1937 %}
    {% if forloop.first %}
    <thead><tr>
      {% for pair in row %}
        <th>{{ pair[0] }}</th>
      {% endfor %}
    </tr></thead><tbody>
    {% endif %}

    {% tablerow pair in row %}
      {{ pair[1] }}
    {% endtablerow %}
  {% endfor %}
  </tbody>
  <tfoot>
    {% for pair in site.data.allHazard_thru1937[0] %}
      <th>{{ pair[0] }}</th>
    {% endfor %}
  </tfoot>
  
</table>
<script>
    $(document).ready(function () {
        $("#hazard-data").DataTable({
            orderMulti: true,
            initComplete: function () {
                this.api()
                    .columns()
                    .every(function () {
                        let column = this;
                        let title = column.footer().textContent;
                        // Create input element
                        let input = document.createElement('input');
                        input.placeholder = title;
                        column.footer().replaceChildren(input);
                        // Event listener for user input
                        input.addEventListener('keyup', () => {
                            if (column.search() !== this.value) {
                                column.search(input.value).draw();
                            }
                        });
                    });
                }
        });
    });
</script>