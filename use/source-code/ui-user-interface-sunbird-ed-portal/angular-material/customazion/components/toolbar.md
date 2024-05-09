# Toolbar

The "[**MatToolbar**](https://v14.material.angular.io/components/toolbar/overview)" is a component provided by Angular Material that serves as a container for various types of content, such as titles, icons, and navigation elements. It is commonly used to create a toolbar at the top of a page for a consistent and organized layout. The `MatToolbar` module is part of the Angular Material library, and it provides styling and layout features to help developers create responsive and visually appealing toolbars in their Angular applications.

Here's a basic example of how you can use the mat-toolbar component in an Angular Material application:

Before writing code in our HTML components, we initially imported and declared the MatChipsModule in "**material.module.ts**".

```typescript
import {MatToolbarModule} from '@angular/material/toolbar';

@NgModule({
  declarations: [
    PillsGridComponent,
    PillItemComponent
  ],
  imports: [
    MatToolbarModule
  ],
  exports: [
    PillsGridComponent,
    PillItemComponent
  ]
})
```

{% code title="collection-player.component" %}
```html
  <mat-toolbar color="primary" class="toolbar-pageback">
    <div class="d-flex flex-ai-center w-below-sm-100 w-above-sm-60">
      <button type="button" mat-mini-fab color="accent"
        class="button-rounded" tabindex="0" (click)="closeCollectionPlayer()"
        attr.aria-label="{{resourceService?.frmelmnts?.btn?.back}}">
        <mat-icon aria-hidden="false" aria-label="Back icon" fontIcon="arrow_back"></mat-icon>
      </button>
      <div class="toolbar-pageback__heading" *ngIf="collectionData">
        <h1 class="mat-title mb-0 sb__ellipsis" tabindex="0" role="heading" aria-level="2">{{collectionData.name}}</h1>
          <div class="toolbar-pageback__metadata">
            <div class="sub-title mat-body-1 mt-4 d-flex flex-ai-center" *ngIf="collectionTreeNodes">
              <span *ngIf="collectionTreeNodes?.data?.board">{{collectionTreeNodes?.data?.board}}</span>
              <span class="dot-divider" *ngIf="collectionTreeNodes?.data?.medium"></span>
              <span *ngIf="collectionTreeNodes?.data?.medium">{{collectionTreeNodes?.data?.medium}}</span>
              <span class="dot-divider" *ngIf="collectionTreeNodes?.data?.gradeLevel"></span>
              <span class="sb__ellipsis whitespace-initial" *ngIf="collectionTreeNodes?.data?.gradeLevel">{{collectionTreeNodes?.data?.gradeLevel}}</span>
            </div>
          </div>
      </div>
    </div>
    <div class="toolbar-pageback__actions" *ngIf="collectionData">
      <button type="button" *ngIf="!isCopyAsCourseClicked" tabindex="0" (click)="onShareLink();sharelinkModal=true;"
      mat-raised-button class="button-rounded mr-8">
      <mat-icon aria-hidden="false" fontIcon="share"></mat-icon> {{resourceService?.frmelmnts?.lbl?.share}}
      </button>
    </div>
  </mat-toolbar>
```
{% endcode %}

And the expected out put is as follows:

<figure><img src="../../../../../../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

**Toolbar with Customization styles**

We established a mixin named "**pageback-toolbar**" in "**\_toolbar-pageback.scss**" situated within the "**mat-themes**" folder. Subsequently, this "**\_toolbar-pageback.scss**"  was imported into the "**includes.scss**" file.

{% code title="_mat-expansion-panel.scss" %}
```scss
@use "@angular/material" as mat;
@use "sass:map";
@forward "./palette";
@forward './buttons';
@use "@project-sunbird/sb-styles/assets/mixins/mixins" as *;

@mixin pageback-toolbar($theme) {

  // Get the color config from the theme.
  $color-config: mat.get-color-config($theme);
  // Get the primary color palette from the color-config.
  $primary: map.get($color-config, 'primary');
  $accent: map.get($color-config, 'accent');
  $warn: map.get($color-config, 'warn');
  $background: map.get($color-config, 'background');

  .mat-toolbar {
    &.toolbar-pageback {
      border-radius: 1.5rem 1.5rem 0 0;
      display: flex;
      align-items: center;
      margin: 0 auto;
      padding:0.5rem 1rem;
      width: 90%;
      gap: 0.5rem;
      min-height: 4rem;
      height: auto;
      flex-wrap: wrap;
      @include respond-below(sm) {
        flex-wrap: wrap;
        height: auto;
        padding: 1rem;
        width: 100%;
        padding-bottom: 2.5rem;
      }
      .thumbnail {
        height: 3rem;
        width: 3rem;
      }
      .mat-title {
        $title-typography: mat.define-typography-config($subheading-2: mat.define-typography-level($font-size: 1rem !important,
            $font-family: inherit, $line-height: normal,
            $font-weight: 700));
        @include mat.typography-level($title-typography, 'subheading-2');
        margin: 0 0 0.5rem 0;
        color: mat.get-color-from-palette($primary, 500-contrast);
        width: 95%;
        white-space: initial;
      }
      &__actions {
        .sb-label-status-error {
          color: mat.get-color-from-palette($warn);
          font-size: 0.75rem;
          background-color:  mat.get-color-from-palette($warn, 100);
        }
      }
      .mat-flat-button.mat-success,
      .mat-raised-button.mat-success,
      .mat-fab.mat-success,
      .mat-mini-fab.mat-success {
        @extend %mat-success;
      }
    }
  }
}
```
{% endcode %}

{% code title="includes.scss" %}
```scss
@import './toolbar-pageback';
```
{% endcode %}

&#x20;A mixin was crafted and then imported into the "**themes.scss**" file within the "**app-themes**" section.

{% code title="themes.scss" %}
```scss
 @include pageback-toolbar($theme);
```
{% endcode %}

The end result will be as follows in differnt themes:

<figure><img src="../../../../../../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../../../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../../../.gitbook/assets/image (53).png" alt=""><figcaption></figcaption></figure>

Remember to check the official [**Angular Material Toolbar documentation**](https://v14.material.angular.io/components/toolbar/overview) for the latest features and detailed information.
