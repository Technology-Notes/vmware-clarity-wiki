This is a quick write up on how we've deprecated APIs in Clarity to ensure stability for a release before removal. It is important to ensure you don't remove or change an exported API without deprecation whenever possible.

## Deprecating an object

To deprecate a class, annotate the object creation with the `@deprecated` jsdoc tag and note the version since it was deprecated. If you know when the object will be removed you can also note the version it will be removed in. The first is an example of not knowing when it will be fully removed, and the second states the expected version to remove.

```
/** @deprecated since 1.0 */
export class ClrOldComponent {}

/** @deprecated since 1.0, to be removed in 2.0 */
export class ClrOldComponent {}
```

## Renaming an object

Sometimes an old object was named improperly or needs to be updated for some reason. The best approach is to update the name of the object at the current definition site, and then redeclare the object in the NgModule file for that given module. In this example, the source is updated to reflect the new API, and then we have to export a new instance of the object with the original name. This is how we changed `Button` to `ClrButton`.

```
# buttons/button-group/button.ts
export class ClrButton { }

# buttons/button-group/button-group.module.ts
import {ClrButton} from "./button";
/** @deprecated since 0.11 */
export class Button extends ClrButton {}
```

This can be a little tricky because there isn't a single pattern for all types of objects. The follow shows examples of how to redeclare a class, enum, interface, and variable. Note that the enum is fully redeclared, due to the nature of enums being static and non-extendable.

```
/* tslint:disable variable-name */
/** @deprecated since 0.11 */
export class Datagrid extends ClrDatagrid {}

/** @deprecated since 0.11 */
export enum SortOrder {
    // Cannot extend an enum so have to redeclare it
    Unsorted = 0,
    Asc = 1,
    Desc = -1
}

/** @deprecated since 0.11 */
export interface Comparator<T> extends ClrDatagridComparatorInterface<any> {}

/* tslint:enable variable-name */
/** @deprecated since 0.11 */
export const DATAGRID_DIRECTIVES = CLR_DATAGRID_DIRECTIVES;
```