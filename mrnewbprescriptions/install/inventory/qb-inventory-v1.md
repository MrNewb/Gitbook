---
description: Inventory Install Steps
icon: box-circle-check
---

# qb-inventory V1

{% embed url="https://github.com/qbcore-framework/qb-inventory/blob/be813ebe73287da7277f1c9589a03f7de213f976/html/js/app.js#L356" %}
Go to this line and add this in qb-inventory/html/js/app.js
{% endembed %}

Add a new "case" under any of the others already listed and paste this in.

<pre class="language-javascript"><code class="lang-javascript">case "medicalprescription":
    return `&#x3C;p>&#x3C;strong>Prescription: &#x3C;/strong>&#x3C;span>${itemData.info.description}&#x3C;/span>&#x3C;/p>`;
case "zombix":
    return `&#x3C;p>&#x3C;strong>Prescription: &#x3C;/strong>&#x3C;span>${itemData.info.description}&#x3C;/span>&#x3C;/p>`;
case "willies":
<strong>    return `&#x3C;p>&#x3C;strong>Prescription: &#x3C;/strong>&#x3C;span>${itemData.info.description}&#x3C;/span>&#x3C;/p>`;
</strong>case "mollis":
    return `&#x3C;p>&#x3C;strong>Prescription: &#x3C;/strong>&#x3C;span>${itemData.info.description}&#x3C;/span>&#x3C;/p>`;
case "realquickioum":
    return `&#x3C;p>&#x3C;strong>Prescription: &#x3C;/strong>&#x3C;span>${itemData.info.description}&#x3C;/span>&#x3C;/p>`;
case "naptimeioum":
    return `&#x3C;p>&#x3C;strong>Prescription: &#x3C;/strong>&#x3C;span>${itemData.info.description}&#x3C;/span>&#x3C;/p>`;
case "rumaierum":
    return `&#x3C;p>&#x3C;strong>Prescription: &#x3C;/strong>&#x3C;span>${itemData.info.description}&#x3C;/span>&#x3C;/p>`;
case "stretchyioum":
    return `&#x3C;p>&#x3C;strong>Prescription: &#x3C;/strong>&#x3C;span>${itemData.info.description}&#x3C;/span>&#x3C;/p>`;
case "jimmyioum":
    return `&#x3C;p>&#x3C;strong>Prescription: &#x3C;/strong>&#x3C;span>${itemData.info.description}&#x3C;/span>&#x3C;/p>`;
case "crowlyioum":
    return `&#x3C;p>&#x3C;strong>Prescription: &#x3C;/strong>&#x3C;span>${itemData.info.description}&#x3C;/span>&#x3C;/p>`;
</code></pre>
