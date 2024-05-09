# Menu

The [**mat-menu**](https://v14.material.angular.io/components/menu/examples) component is used to create a menu in Angular applications following the Material Design guidelines. It typically consists of a trigger element (e.g., a button) and a hidden menu that appears when the trigger is interacted with (e.g., clicked).

Before writing code in our HTML components, we initially imported and declared the MatMenuModule in "**groups.module.ts**".

```typescript
import {MatMenuModule} from '@angular/material/menu';

@NgModule({
  declarations: [
    // code here
  ],
  imports: [
    MatMenuModule
  ],
  exports: [
  ]
})
```

Here's a breakdown of the `mat-menu` component:

**Trigger Element:** The trigger element is the UI element that, when interacted with, opens the associated menu. It can be any clickable element like a button or an icon. In the example from before, the trigger element is a button with the `[matMenuTriggerFor]` directive pointing to the `mat-menu`.

{% code title="group-header.component.html" %}
```html
<button mat-icon-button [matMenuTriggerFor]="menu" id="group-actions" tabindex="0" (click)="addTelemetry('kebab-menu')">
    <mat-icon>more_vert</mat-icon>
</button>
```
{% endcode %}

**Menu Content:** The content of the menu is defined within the `<mat-menu>` tags. You can include various items inside the menu, such as `mat-menu-item` for clickable items within the menu.

{% code title="group-header.component.html" %}
```html
<mat-menu #menu="matMenu">
  <div *ngIf="groupData?.isAdmin">
    <div *ngIf="groupData?.active">
      <button mat-menu-item (click)="editGroup();addTelemetry('edit-group', '', { type: UPDATE_GROUP})" tabindex="0">{{resourceService?.frmelmnts?.lbl?.editGroup}}</button>
      <button mat-menu-item (click)="toggleModal(true, 'deActivate')" tabindex="0">{{resourceService?.frmelmnts?.btn?.deactivategrp}}</button>
      <button mat-menu-item (click)="enableDiscussionForum()" tabindex="0" *ngIf="forumIds.length === 0">{{resourceService?.frmelmnts?.lbl?.enableDiscussionForum}}</button>
    </div>
  </div>
  <div *ngIf="groupData?.isCreator">
    <button mat-menu-item class="color-warn" (click)="toggleModal(true, 'delete');" tabindex="0">{{resourceService?.frmelmnts?.lbl?.deleteGroup}}</button>
  </div>
</mat-menu>
```
{% endcode %}

**Configuration:** You can configure the menu by using various options. For example, you can use `[xPosition]` and `[yPosition]` to control the position of the menu, and `[hasBackdrop]` to specify whether clicking outside the menu should close it.

```html
<mat-menu #menu="matMenu" [xPosition]="'before'" [yPosition]="'below'" [hasBackdrop]="false">
  <!-- menu items go here -->
</mat-menu>
```

The anticipated output is as follows:

<figure><img src="../../../../../../.gitbook/assets/image (68).png" alt=""><figcaption></figcaption></figure>

**Menu with custom styles**

To apply custom styles, we create an HTML class named "**custom-menu**" and by utilizing this class, we override the existing styles.

```html
<mat-menu #menu="matMenu" class="custom-menu"> 
    <!-- menu items go here -->
</mat-menu>
```

```scss
.custom-menu{
  &.mat-menu-panel {
    box-shadow: 0 0.1875rem 0.3125rem 0.25rem #0000000d;
    padding: 0.5rem;
    border-radius: 1rem;
    .mat-menu-content {
      padding: 0;
      .mat-menu-item {
        font-size: .875rem;
        height: 36px;
        line-height: 36px;
        border-radius: 1rem;
        &:hover {
            background: var(--color-primary-50);
        }
      }
    }
  }
}
```

And the expected result is

<figure><img src="../../../../../../.gitbook/assets/image (69).png" alt=""><figcaption></figcaption></figure>

Remember to check the official [**Angular Material Menu documentation**](https://v14.material.angular.io/components/menu/overview) for the latest features and detailed information.
