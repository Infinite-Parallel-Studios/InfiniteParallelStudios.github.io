---
icon: fas fa-envelope
order: 5
---

{%- assign has_booking = false -%}
{%- if site.portfolio.booking_url and site.portfolio.booking_url != "" -%}{%- assign has_booking = true -%}{%- endif -%}
{%- assign has_form = false -%}
{%- if site.portfolio.contact_form_endpoint and site.portfolio.contact_form_endpoint != "" -%}{%- assign has_form = true -%}{%- endif -%}

Hiring for a forward deployed or AI engineering role, or have a project in mind? {% if has_booking and has_form %}Book a time to talk or send me a note, and I'll get back to you.{% elsif has_booking %}Book a time to talk.{% else %}Send me a note and I'll get back to you.{% endif %}

{% if has_booking and has_form %}
## Book a call

{% include booking.html %}

## Send a message
{% else %}{% include booking.html %}{% endif %}

{% include contact-form.html %}

You can also find my work on [GitHub](https://github.com/Infinite-Parallel-Studios).
