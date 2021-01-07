# BlazorDataBinding
This shows an example of how you can create @bind attribute on your custom blazor components.

In order to do this, you will need the following things:

1. One static `BindAttributes` class annotated with `[BindElement]` attributes for each of your targeted components, it needs the following arguments:
   1. `element` is a string that matches exactly the name of your custom component;
   1. `suffix` can remain null, we don't need it;
   1. `valueAttribute` is a string that matches exactly the name of the public parameter in your custom component, this is what the @bind keyword will chain to;
   1. `changeAttribute` is a string that matches exactly the name of the public envent callback in your custom component, this will notify your parent component that the value has been updated.
1. One custom component you have built, outfitted with the following things:
   1. a public parameter to hold your bound value, its name should match exactly the `valueAttribute` you've given to this component's `[BindElement]` annotation;
   1. one public event callback parameter which will be used to trigger the bind event and pass the bound value to its parent, its name should match exactly the `changeAttribute` you've given to this component's `[BindElement]` annotation and it should handle the type of your public parameter;
   1. a private property which will cascade the private parameter's value down to the editors in your component and back up to the public parameter
      - the getter of this property will retrieve the value of your public parameter
      - the setter of this property will invoke the event callback to which this component's `[BindElement]` annotation subscribes.
    
After that, you can use the @bind attribute on your custom component as if it was a regular input.

You can refer to the project's source code for a working example of this mechanic.
