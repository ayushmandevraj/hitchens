{% macro errorList(errors) %}
    {% if errors %}
        <ul class="errors">
            {% for error in errors %}
                <li>{{ error }}</li>
            {% endfor %}
        </ul>
    {% endif %}
{% endmacro %}

{% from _self import errorList %}

<form method="post" action="" accept-charset="UTF-8">
    {{ csrfInput() }}
    <input type="hidden" name="action" value="contact-form/send">
    {{ redirectInput('contact/thanks') }}

    <h3><label for="from-name">Your Name</label></h3>
    <input id="from-name" type="text" name="fromName" value="{{ message.fromName ?? '' }}">
    {{ message is defined and message ? errorList(message.getErrors('fromName')) }}

    <h3><label for="from-email">Your Email</label></h3>
    <input id="from-email" type="email" name="fromEmail" value="{{ message.fromEmail ?? '' }}">
    {{ message is defined and message ? errorList(message.getErrors('fromEmail')) }}

    <h3><label for="subject">Subject</label></h3>
    <input id="subject" type="text" name="subject" value="{{ message.subject ?? '' }}">
    {{ message is defined and message ? errorList(message.getErrors('subject')) }}

    <h3><label for="message">Message</label></h3>
    <textarea rows="10" cols="40" id="message" name="message">{{ message.message ?? '' }}</textarea>
    {{ message is defined and message ? errorList(message.getErrors('message')) }}

    <input type="submit" value="Send">
</form>
