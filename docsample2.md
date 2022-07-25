# Объект $ref в OpenAPI Specification

При документировании API нередко приходится использовать одни и те же определения в описаниях различных ресурсов. Для таких случаев предусмотрена возможность создавать отдельные фрагменты кода и использовать их повторно при необходимости. В OpenAPI 3.0 вы можете ссылаться на определение, расположенное в любом месте схемы, используя ключевое слово `$ref`.

Например, у вас есть схема, которую вы хотите использовать в качестве ответа внутри объекта `responses`:

<table>
	<thead>
		<tr>
			<th>JSON Example</th>
			<th>YAML Example</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>
			<pre>
<code>&quot;components&quot;: {
  &quot;schemas&quot;: {
    &quot;user&quot;: {
      &quot;properties&quot;: {
        &quot;quot;id&quot;: {
          &quot;type&quot;: &quot;integer&quot;
        },
        &quot;name&quot;: {
          &quot;type&quot;: &quot;string&quot;
        }
      }
    }
  }
}
</code></pre>
			</td>
			<td>
			<pre>
<code>components:
  schemas:
    User:
      properties:
        id:
          type: integer
        name:
          type: string
</code></pre>
			</td>
		</tr>
	</tbody>
</table>

Чтобы сослаться на эту схему, добавьте объект `$ref` с указанием пути к ответу:
<table>
	<thead>
		<tr>
			<th>JSON Example</th>
			<th>YAML Example</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>
			<pre>
<code>&quot;responses&quot;: {
  &quot;200&quot;: {
    &quot;description&quot;: &quot;The response&quot;,
    &quot;schema&quot;: {
      &quot;$ref&quot;: &quot;#/components/schemas/user&quot; 
    }
  }
}
</code></pre>
			</td>
			<td>
			<pre>
<code>responses:
  &#39;200&#39;:
    description: The response
    schema: 
      $ref: &#39;#/components/schemas/User&#39;
</code></pre>
			</td>
		</tr>
	</tbody>
</table>

Значение объекта $ref регулируется спецификацией [JSON Reference](https://tools.ietf.org/html/draft-pbryan-zyp-json-ref-03), а указание пути после `#` регулируется спецификацией [JSON Pointer](https://tools.ietf.org/html/rfc6901). Эта нотация позволяет определять путь к целевому файлу или к части файла, на которую необходимо сослаться. 