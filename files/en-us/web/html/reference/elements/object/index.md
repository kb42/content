---
title: "<object>: The External Object element"
slug: Web/HTML/Reference/Elements/object
page-type: html-element
browser-compat: html.elements.object
sidebar: htmlsidebar
---

The **`<object>`** [HTML](/en-US/docs/Web/HTML) element represents an external resource, which can be treated as an image, a nested browsing context, or a resource to be handled by a plugin.

{{InteractiveExample("HTML Demo: &lt;object&gt;", "tabbed-standard")}}

```html interactive-example
<object
  type="video/mp4"
  data="/shared-assets/videos/flower.mp4"
  width="250"
  height="200"></object>
```

## Attributes

This element includes the [global attributes](/en-US/docs/Web/HTML/Reference/Global_attributes).

- `archive` {{deprecated_inline}}
  - : A space-separated list of URIs for archives of resources for the object.
- `border` {{deprecated_inline}}
  - : The width of a border around the control, in pixels.
- `classid` {{deprecated_inline}}
  - : The URI of the object's implementation. It can be used together with, or in place of, the **data** attribute.
- `codebase` {{deprecated_inline}}
  - : The base path used to resolve relative URIs specified by **classid**, **data**, or **archive**. If not specified, the default is the base URI of the current document.
- `codetype` {{deprecated_inline}}
  - : The content type of the data specified by **classid**.
- `data`
  - : The address of the resource as a valid URL. At least one of **data** and **type** must be defined.
- `declare` {{deprecated_inline}}
  - : The presence of this Boolean attribute makes this element a declaration only. The object must be instantiated by a subsequent `<object>` element. Repeat the `<object>` element completely each time the resource is reused.
- `form`
  - : The form element, if any, that the object element is associated with (its _form owner_). The value of the attribute must be an ID of a {{HTMLElement("form")}} element in the same document.
- `height`
  - : The height of the displayed resource, as in {{cssxref("&lt;integer&gt;")}} in {{glossary("CSS pixel", "CSS pixels")}}.
- `name`
  - : The name of valid browsing context (HTML5), or the name of the control (HTML 4). The name becomes a property of the {{domxref("Window")}} and {{domxref("Document")}} objects, containing a reference to the embedded window or the element itself.
- `standby` {{deprecated_inline}}
  - : A message that the browser can show while loading the object's implementation and data.
- `type`
  - : The [content type](/en-US/docs/Glossary/MIME_type) of the resource specified by **data**. At least one of **data** and **type** must be defined.
- `usemap` {{deprecated_inline}}
  - : A hash-name reference to a {{HTMLElement("map")}} element; that is a '#' followed by the value of a [`name`](/en-US/docs/Web/HTML/Reference/Elements/map#name) of a map element.
- `width`
  - : The width of the display resource, as in {{cssxref("&lt;integer&gt;")}} in {{glossary("CSS pixel", "CSS pixels")}}.

## Examples

### Embed a video

#### HTML

```html
<object
  type="video/webm"
  data="/shared-assets/videos/flower.webm"
  width="600"
  height="140">
  <img
    src="/shared-assets/images/examples/flowers.jpg"
    alt="Some beautiful flowers" />
</object>
```

#### Result

{{EmbedLiveSample("Embed a video")}}

If the video in the example fails to load, the user will be provided with an image as fallback content. The {{HTMLElement("img")}} tag is used to display an image. We include the `src` attribute set to the path to the image we want to embed. We also include the `alt` attribute, which provides the image with an accessible name. If the image also fails to load, the content of the `alt` attribute will be displayed.

## Technical summary

<table class="properties">
  <tbody>
    <tr>
      <th scope="row">
        <a href="/en-US/docs/Web/HTML/Guides/Content_categories">Content categories</a>
      </th>
      <td>
        <a href="/en-US/docs/Web/HTML/Guides/Content_categories#flow_content">Flow content</a>;
        <a href="/en-US/docs/Web/HTML/Guides/Content_categories#phrasing_content">phrasing content</a>;
        <a href="/en-US/docs/Web/HTML/Guides/Content_categories#embedded_content">embedded content</a>, palpable content; if the element has a
        <a href="#usemap"><code>usemap</code></a> attribute, <a href="/en-US/docs/Web/HTML/Guides/Content_categories#interactive_content">interactive content</a>;
        <a href="/en-US/docs/Web/HTML/Guides/Content_categories#listed">listed</a>,
        <a href="/en-US/docs/Web/HTML/Guides/Content_categories#submittable">submittable</a>
        <a href="/en-US/docs/Web/HTML/Guides/Content_categories#form-associated_content">form-associated</a> element.
      </td>
    </tr>
    <tr>
      <th scope="row">Permitted content</th>
      <td>
        zero or more {{HTMLElement("param")}} elements, then
        <a href="/en-US/docs/Web/HTML/Guides/Content_categories#transparent_content_model">transparent</a>.
      </td>
    </tr>
    <tr>
      <th scope="row">Tag omission</th>
      <td>None, both the starting and ending tag are mandatory.</td>
    </tr>
    <tr>
      <th scope="row">Permitted parents</th>
      <td>
        Any element that accepts <a href="/en-US/docs/Web/HTML/Guides/Content_categories#embedded_content">embedded content</a>.
      </td>
    </tr>
    <tr>
      <th scope="row">Implicit ARIA role</th>
      <td>
        <a href="https://w3c.github.io/html-aria/#dfn-no-corresponding-role">No corresponding role</a>
      </td>
    </tr>
    <tr>
      <th scope="row">Permitted ARIA roles</th>
      <td>
        <a href="/en-US/docs/Web/Accessibility/ARIA/Reference/Roles/application_role"><code>application</code></a>, <a href="/en-US/docs/Web/Accessibility/ARIA/Reference/Roles/document_role"><code>document</code></a>, <a href="/en-US/docs/Web/Accessibility/ARIA/Reference/Roles/img_role"><code>img</code></a>
      </td>
    </tr>
    <tr>
      <th scope="row">DOM interface</th>
      <td>{{domxref("HTMLObjectElement")}}</td>
    </tr>
  </tbody>
</table>

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- {{HTMLElement("embed")}}
- {{HTMLElement("param")}}
