# Property Group Mediator

The Property Group mediator is similar to the [Property Mediator]({{base_path}}/reference/mediators/property-mediator). It sets or removes properties on the message context flowing through synapse. However, unlike the Property mediator, the Property Group mediator handles multiple properties as a
group. You can select the property action (i.e., whether the property
must be added to or removed from the message context) for each
individual property. Therefore, in a scenario where you need to
set/remove multiple properties, you can add a single Property Group
Mediator configuration instead of multiple Property Mediator
configurations.

## Syntax

```
<propertyGroup>
    <property name="name0" value="value0"/>
    <property name="name1" value="value1"/>
    <property name="name2" value="value2"/>
    ........
</propertyGroup>
```

## Configuration

The Property Group Mediator configuration includes a description and a set of properties grouped together.

In the source view, multiple Property Mediator configurations are
enclosed within the `<propertyGroup>` element. You can
also add a description in the opening element. (e.g., `<propertyGroup description="A group of properties to include in the greeting message">`).

In the design view, you can configure the Property Group Mediator as
follows:

-   Enter a meaningful description for the property group in the
    **Description** field.
-   To add a new property, click the **+ Add Parameter** text button.
    As a result, the **Property Mediator** dialog box opens. Here, you
    can configure a custom property.
-   To remove a property, click the delete icon next to the property.
    ![]({{base_path}}/assets/img/integrate/mediators/119134127/119134161.png)
-   To arrange the properties in the required order within the property
    group configuration, you can drag and drop the properties in the desired order.

## Example

The following Property Group Mediator configuration adds the
`From` , `Message` , and `To` properties to the message context. It also removes
the `MessageID` property from the context. All four properties are handled together as a group.

``` xml
<propertyGroup description="A group of properties to include in the greeting.">
    <property action="remove" name="MessageID" scope="default"/>
    <property name="From" scope="default" type="STRING" value=""/>
    <property name="Message" scope="default" type="STRING" value="Welcome to XXX group!"/>
    <property name="To" scope="default" type="STRING" value=""/>
</propertyGroup>
```
