# Context

lib/accesslib.php

* Context: system, courses, activity, blocks...
  * It's like a tree, you can have many contexes at once \(System -&gt; Course -&gt; Activity -&gt; ..\)

### Context types

* context\_coursecat
* context\_course
* context\_module
* context\_block
* context\_helper
* context\_system
* context\_user

## Get context infomation array by context id

{% tabs %}
{% tab title="PHP" %}
```php
list($context, $course, $cm) = get_context_info_array($contextid);
```
{% endtab %}
{% endtabs %}

## Get the course context by course id

```php
$coursecontext = context_course::instance($courseid);
echo "Context id: ".$coursecontext->id;
```

* `get_context_instance`is debricated

## Get context of parent

```php
class block_course_checker extends block_base {
    // [..]
    $this->instance->parentcontextid
```

## Get context with direct db query

{% hint style="warning" %}
If you can prevent this, do it.
{% endhint %}

```php
$context = $DB->get_record('context', ['instanceid' => $course->id, 'contextlevel' => CONTEXT_COURSE]);
$blockexists = $DB->get_record('block_instances', [
        'blockname' => self::BLOCK_TYPE_COMPLETIONPROGRESS,
        'parentcontextid' => $context->id
]);
```

## 

