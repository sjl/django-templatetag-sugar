django-templatetag-sugar
========================

A library to make writing templatetags in Django sweet.

Install it:

    pip install -e git://github.com/alex/django-templatetag-sugar.git#egg=templatetag_sugar

Put this sucker into `yourapp/templatetags/some_tags.py` and `{% load some_tags %}`
in your templates:

    from django import template
    from templatetag_sugar.register import tag
    from templatetag_sugar.parser import Name, Variable, Constant, Optional

    register = template.Library()

    @tag(register, [Constant("for"), Variable(), Optional([Constant("as"), Name()])]):
    def example_tag(context, val, asvar=None):
        if asvar:
            context[asvar] = val
            return ""
        else:
            return val

