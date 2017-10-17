# RUVENTS API Bundle

## Routing

```yaml
_api:
    resource: '@AppBundle/Controller/Api/'
    type:     annotation
    prefix:   /api
    defaults:
        _format: json
        # _ruvents_api attribute enables api listeners for this route
        _ruvents_api: true
```

## Controller

```php
<?php

namespace AppBundle\Controller\Api;

use Ruvents\ApiBundle\Annotations as Api;
use Ruvents\ApiBundle\Controller\AbstractApiController;
use Sensio\Bundle\FrameworkExtraBundle\Configuration\Method;
use Sensio\Bundle\FrameworkExtraBundle\Configuration\Route;

/**
 * @Route("/test")
 */
class TestController extends AbstractApiController
{
    /**
     * @Method("GET")
     * @Route("")
     * @Api\Doc("Test method", requiresAuth=true, description="<p>Test method description.</p>",
     *     params={@Api\Param("id", required=true, format="int", description="<p>Description.</p>")},
     *     block="test", displayRoles={"ROLE_API_TEST"}
     * )
     */
    public function indexAction()
    {
        return ['test' => 1];
    }
}
```

## Templating

```yaml
twig:
    paths:
        "%kernel.project_dir%/vendor/ruvents/api-bundle/Resources/views": RuventsApiOriginal
```

```twig
{# app/Resources/RuventsApiBundle/views/docs.html.twig #}

{% extends '@RuventsApiOriginal/docs.html.twig' %}

{% block title 'Website API' %}

{% block test %}
    Override the whole method card
{% endblock %}

{% block test_description %}
    Override method description
{% endblock %}

{% block test_param_id_description %}
    Override parameter description
{% endblock %}
```