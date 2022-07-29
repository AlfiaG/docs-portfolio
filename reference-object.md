# Объект $ref в OpenAPI Specification
 
При документировании API нередко приходится использовать одни и те же определения в описаниях различных ресурсов. Для таких случаев предусмотрена возможность создавать отдельные фрагменты кода и использовать их повторно при необходимости. В OpenAPI 3.0 вы можете ссылаться на определение, расположенное в любом разделе документа, используя ключевое слово `$ref`.
 
Например, у вас есть схема, которую вы хотите использовать в качестве ответа внутри объекта `responses`:
 
<table>
   <thead>
       <tr>
           <th>Пример в JSON</th>
           <th>Пример в YAML</th>
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
           <th>Пример в JSON</th>
           <th>Пример в YAML</th>
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
 
Значение объекта `$ref` соответствует нотации [ссылки JSON](https://tools.ietf.org/html/draft-pbryan-zyp-json-ref-03), а указание пути после `#` соответствует нотации [указателя JSON](https://tools.ietf.org/html/rfc6901). Эта нотация позволяет обозначить путь к целевому файлу или к фрагменту файла, на который необходимо сослаться. В предыдущем примере путь `#/components/schemas/User` начинается с верхнего уровня текущего документа, а затем один за другим определяются значения полей `components`, `schemas` и `User`.

## Синтаксис объекта $ref

Согласно спецификации [RFC3986](https://tools.ietf.org/html/rfc3986), значение строки `$ref` должно содержать идентификатор URI, определяющий расположение объекта JSON, на который делается ссылка. Если значение строки нарушает синтаксис идентификатора URI, возникают ошибки при чтении, и любые объекты в ссылке, кроме `$ref`, игнорируются.

Примеры ссылок JSON для различных случаев применения:
- **Локальная ссылка**  – `$ref: '#/definitions/myElement'`. Хэш `#` направляет на верхний уровень текущего документа, затем один за другим определяются значения элементов `definitions` и `myElement`.
- **Внешняя ссылка** – `$ref: 'document.json'`. Ссылка на документ, располагающийся на том же сервере.
  - **Фрагмент документа, расположенного в той же папке** – `$ref: 'document.json#/myElement'`
  - **Фрагмент документа, расположенного в корневой папке** – `$ref: '../document.json#/myElement'`
  - **Фрагмент документа расположенного в другой папке** – `$ref: '../another-folder/document.json#/myElement'`
- **Ссылка URL** – `$ref: 'http://path/to/your/resource`. Для докуметов на другом сервере.
  - **Фрагмент документа, расположенного на другом сервере** – `$ref: 'http://path/to/your/resource.json#/myElement'`
  - **Документ на другом сервере, использующем такой же протокол (например, HTTP или HTTPS)** – `$ref: '//anotherserver.com/files/example.json'`

Обратите внимание: локальные ссылки в YAML должны быть заключены в одиночные кавычки: `'#/components/schemas/User'`. Без кавычек они будут отформатированы как комментарии.

## Поля объекта $ref

| **Название поля** | **Тип** | **Описание** |
| --- | --- | --- |
| `$ref` | `строка` | *ОБЯЗАТЕЛЬНОЕ ПОЛЕ*. Идентификатор ссылки. *ДОЛЖНО* быть представлено в форме URI. |
| `summary` | `строка` | Краткое резюме, которое по умолчанию переопределяет значение поля `summary` того объекта, на который делается ссылка. Если тип объекта, на который делается ссылка, не предусматривает поле `summary`, это поле игнорируется. |
| `description` | `строка` | Описание, которое по умолчанию переопределяет значение поля `description` того объекта, на который делается ссылка. Если тип объекта, на который делается ссылка, не предусматривает поле `description`, это поле игнорируется. |

К этому объекту не могут быть добавлены дополнительные свойства. Любые добавленные свойства будут игнорироваться. Обратите внимание, что данное ограничение составляет основное различие между объектами `$ref` и [объектами Schema](https://spec.openapis.org/oas/latest.html#schemaObject) с ключевым словом `$ref`.

## Символы, требующие экранирования

Символы `/` и `~` – специальные символы в указателе JSON, которые требуют экранирования, когда используются буквально (например, при обозначении пути к объекту).

| **Символ** | **Экранирование** |
| :---: | :---: |
| ~ | ~0 |
| / | ~1 |

Например, так будет выглядеть путь `/blogs/{blog_id}/new~posts`:

```
$ref: '#/paths/~1blogs~1{blog_id}~1new~0posts'
```

## Где может быть использован объект $ref

Ошибочно считать, что объект `$ref` можно использовать в любом месте документа OpenAPI. Его можно использовать только в тех объектах, для которых в [спецификации OpenAPI](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md) оговорено, что значение свойства может быть ссылкой. Например, нельзя использовать `$ref` в объектах `info` и `paths`:

```yaml
openapi: 3.0.0
# Неправильно!
info:
  $ref: info.yaml
paths:
  $ref: paths.yaml

```

Однако вы можете использовать `$ref` в полях внутри свойства `paths`:

```yaml
paths:
  /users:
    $ref: '../resources/users.yaml'
  /users/{userId}:
    $ref: '../resources/users-by-id.yaml'
```

## Объект $ref и одноуровневые элементы

Любой элемент на одном уровне с объектом `$ref` игнорируется, потому что `$ref` замещает все элементы на своем уровне тем определением, на которое отсылает. В примере ниже свойства `description` и `default` игнорируются, поэтому схема содержит только свойство `Date`, на которое сделана ссылка.

```yaml
components:
  schemas:
    Date:
      type: string
      format: date

    DateWithExample:
      $ref: '#/components/schemas/Date'
      description: Date schema extended with a `default` value... Or not?
      default: 2000-01-01
```

Источники:
- [OpenAPI Guide. Using $ref](https://swagger.io/docs/specification/using-ref/)
- [OpenAPI Specification v3.1.0](https://spec.openapis.org/oas/latest.html)