---
layout: post
title: Django, ORM, UML and ERD...WTF?!?!
---

Once upon a time (Few days ago) I forked [django-yuml] and writing its code I realized: *"Why don't generalize this project?"*.

##The Idea
Actually, I'm focusing on entities and relations: the *structural* UML point of view. From Models to Class Diagramm I need basically three steps:

![Activity][ser]

#Syntetize et Impera
Analizing the core a question pop up: *"How can I syntetize a django's
model?"* or rather *"Which model's elements I need to draw it and How can I use them?"*
To answer to these innocent questions we need first of all to choose a *standard* grafical model.
By definition the **O**bject-**R**elational **M**apping is:

> a programming technique for converting data between incompatible type systems
> in object-oriented programming languages. [...] 

> The heart of the problem is translating the logical representation of the
> objects into an atomized form
> that is capable of being stored on the database while somehow preserving the
> properties of the objects and their relationships so that they can be reloaded
> as an object when needed.

> <cite>[Wikipedia]</cite>

So our *standard* can't be *UML Class Diagram* neither *ERD*.
Luckly [UML] has the flexibily to redesign a **Meta-Model** to fit our needs.

This is my basic proposal:

![MetaModel][mm]

and this is the **dictionary** example:

{% highlight python %}
class AbstractSyntetizr(object):
    @classmethod
    def synt_applications(kls, applications):
        return [kls.synt_application(e) for e in applications]

    @classmethod
    def synt_application(kls, application):
        raise NotImplementedError("Abstract Method")

    @classmethod
    def synt_models(kls, models):
        return [kls.synt_model(e) for e in models]

    @classmethod
    def synt_model(kls, model):
        raise NotImplementedError("Abstract Method")

    @staticmethod
    def label(model):
        return model._meta.app_label+'.'+model._meta.object_name

    @classmethod
    def synt_fields(kls, fields):
        return [kls.synt_field(e) for e in fields]

    @classmethod
    def synt_field(kls, field):
        raise NotImplementedError("Abstract Method")


from django.db.models.loading import get_models, get_app, get_model
class DictSynt(Syntetizr):
    @classmethod
    def synt_application(kls, application):
        if type(application) is str:
            application = get_app(application)
        return [kls.synt_models(e) for e in get_models(application)]

    @classmethod
    def synt_model(kls, model):
        if type(model) is str:
            model = get_model(model)
        return {
            'name'    : kls.label(model),
            'parents' : [kls.label(p) for p in model._meta.parents],
            'field'   : kls.synt_fields(model._meta.fields),
        }

    @classmethod
    def synt_field(kls, field):
        return field_dict = {
            'primary'  : field.pk,
            'name'     : field.name,
            'type'     : field.__class__.__name__,
            'auto'     : field.auto_created,
            'unique'   : field.unique,
            'default'  : field.default,
            'null'     : field.null,
            'relation' : kls.synt_relation(field.rel),
        }

    @classmethod
    def synt_relation(kls, relation):
        if not relation:
            return {}
        return {
            'to'          : kls.label(relation.to)
            'name'        : relation.related_name,
            'symmetrical' : getattr(relation, 'symmetrical', False),
            'multiple'    : relation.multiple,
            'through'     : getattr(relation, 'through', None),
        }

{% endhighlight %}

[django-yuml]: https://github.com/z4r/django-yuml
[wikipedia]: http://en.wikipedia.org/wiki/Object-relational_mapping
[UML]: http://www.omg.org/spec/UML/2.0/

[ser]: http://yuml.me/diagram/scruffy/activity/(start)->(Syntetizer)->(Encoder)->(Renderer)->(end)
[mm]: http://yuml.me/diagram/scruffy/class/[App|name]1++->[Model],[Model|name]1++->*[Field|name;dataType;primary;default;null;unique;],[Model]->parents[Model],[Relation|multiple;symmetrical]<0..1-++1[Field],[Relation]related_name-to>[Model],[Relation]->through[Model]
