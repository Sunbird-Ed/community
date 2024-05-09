# Chips

"[**Mat chips**](https://v14.material.angular.io/components/chips/overview)" are components provided by Angular Material, designed for creating visually appealing and interactive chips or tags in a user interface. These chips are commonly used to represent discrete pieces of information or items that can be selected, filtered, or removed. Key features and characteristics of mat chips typically include:

1. **Visual Representation**: Mat chips provide a visually distinct representation of items or categories in the form of small, rounded rectangles. Each chip typically contains text or other content.
2. **Interactive**: Users can interact with mat chips, such as selecting, deselecting, or removing them by clicking or tapping.
3. **Selection State**: Mat chips often support selection states, making them suitable for implementing tags, filters, or multi-selection options.
4. **Custom Styling**: Angular Material provides theming and styling options that allow you to customize the appearance of mat chips to match your application's design and branding.
5. **Accessibility**: Mat chips are designed with accessibility in mind, ensuring keyboard navigation and screen reader compatibility.

Mat chips are commonly used in various contexts, including:

* **Tags**: Representing tags associated with an item, post, or category.
* **Filters**: Allowing users to filter and narrow down options.
* **Selection Controls**: Enabling multi-selection of items in a list.
* **Input Components**: Creating dynamic input fields with chips for adding items.

Here's a basic example of how you can use the mat-chip component in an Angular Material application:

```html
<mat-chip-list aria-label="Fish selection">
  <mat-chip>One fish</mat-chip>
  <mat-chip>Two fish</mat-chip>
  <mat-chip color="primary" selected>Primary fish</mat-chip>
  <mat-chip color="accent" selected>Accent fish</mat-chip>
</mat-chip-list>
```

The resulting output will appear as follows:

<figure><img src="../../../../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

### Customization

In our application, we have implemented customized chips.

Before writing code in our HTML components, we initially imported and declared the MatChipsModule in "**pills-grid.module.ts**".

```typescript
import { MatChipsModule } from '@angular/material/chips';

@NgModule({
  declarations: [
    PillsGridComponent,
    PillItemComponent
  ],
  imports: [
    MatChipsModule
  ],
  exports: [
    PillsGridComponent,
    PillItemComponent
  ]
})
```

After importing the module, we proceeded to add the chips code in "**pill-item.component.html**"

```html
<mat-chip-list>
    <mat-chip aria-label="subjects selection" class="item" (click)="onClick($event)" role="button" tabindex="0">
      <span *ngIf="icon" [ngStyle]="{'background-color':theme?.iconBgColor}" class="mr-8 img">
        <img alt="{{name}} icon" src="{{icon}}" class="w-100">
      </span>
      <label [ngStyle]="{'color':theme?.pillTextColor}" class="mb-0" *ngIf="name">{{name}}</label>
    </mat-chip>
  </mat-chip-list>
```

We established a mixin named "**theme-mat-chips**" in "**\_mat-chips.scss**" situated within the "**mat-themes**" folder. Subsequently, this "**\_mat-chips.scss**"  was imported into the "**includes.scss**" file.

{% code title="_mat-chips.scss" %}
```scss
@mixin theme-mat-chips($theme) {
  // Get the color config from the theme.
  $color-config: mat.get-color-config($theme);
  // Get the primary color palette from the color-config.
  $primary: map.get($color-config, 'primary');
  $accent: map.get($color-config, 'accent');
  $warn: map.get($color-config, 'warn');
  $background: map.get($color-config, 'background');

  .mat-card .mat-chip.mat-standard-chip{
    background-color: mat.get-color-from-palette($background, status-bar);
  }
  .mat-chip.mat-standard-chip{
    background-color: mat.get-color-from-palette($background, background);
  }
  .mat-chip.mat-standard-chip{
    font-weight: 700;
    border-radius: 0.25rem;
    padding: 0.5rem 0.75rem;
    font-size: inherit;
    &::after{
      background: none;
    }
  }
  .mat-chip-list-wrapper{
    justify-content: center;
  }
}
```
{% endcode %}

{% code title="includes.scss" %}
```scss
@import './mat-chips';
```
{% endcode %}

A mixin was crafted and then imported into the "**themes.scss**" file within the "**app-themes**" section.

{% code title="themes.scss" %}
```scss
@include theme-mat-chips($app-themes);
```
{% endcode %}

The end result will be as follows:

<figure><img src="../../../../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

Mat chips are a versatile and user-friendly way to manage and display categorized information or user selections in your application.
