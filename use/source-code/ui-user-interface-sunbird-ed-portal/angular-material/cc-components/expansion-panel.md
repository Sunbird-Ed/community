# Expansion Panel

A "[**mat expansion panel**](https://v14.material.angular.io/components/expansion/overview)" is a user interface component provided by Angular Material that enables the creation of expandable and collapsible panels or sections of content. These panels are typically used to display structured information or content that can be expanded to reveal additional details or collapsed for a more concise view. Key features and characteristics of mat expansion panels often include:

1. **Expand and Collapse**: Users can expand and collapse the panel by clicking on a header or trigger element, revealing or hiding the panel's content.
2. **Header and Content**: Each expansion panel consists of a header and content section. The header typically contains a title, icon, or other trigger elements, while the content section displays additional information.
3. **Accordion Behavior**: Mat expansion panels can be configured to behave as an accordion, allowing only one panel to be open at a time, or in a non-accordion mode where multiple panels can be open simultaneously.
4. **Custom Styling**: Angular Material provides theming and styling options to customize the appearance of mat expansion panels to match your application's design and branding.
5. **Accessibility**: Mat expansion panels are designed with accessibility in mind, ensuring keyboard navigation and screen reader compatibility.

Mat expansion panels are commonly used in various contexts, including:

* **FAQ Sections**: To provide expandable answers to frequently asked questions.
* **Detailed Information**: For revealing additional details or descriptions.
* **Settings and Configuration**: In user interfaces where settings can be expanded for customization.

We have already imported **MatExpansionModule** in **material.module.ts**

```typescript
import {MatExpansionModule} from '@angular/material/expansion';
```

We have written html code in **faq.component.html**

```html
<mat-accordion>
  <mat-expansion-panel class="mat-app-background2" (closed)="toggleGroup(i,$event)" (opened)="toggleGroup(i,$event)" role="button" [attr.aria-expanded]="panelOpenState === true ? true : false" *ngFor="let faq of faqs; let i = index">
    <mat-expansion-panel-header>
      <mat-panel-title [ngClass]="panelOpenState === false ? '' : 'color-accent'">
        {{faq?.topic}}
      </mat-panel-title>
    </mat-expansion-panel-header>
    <div>
    <div class="text-left mat-body-2 mb-16" [innerHtml]="faq.description"></div>
    <fieldset *ngIf="!isNoClicked && !isYesClicked">
      <legend class="mat-body-2 my-8 pb-0 text-center">{{data?.constants?.helpMsg}}&lrm;</legend>
      <div class="d-flex flex-jc-center">
        <button mat-raised-button type="button" class="button-rounded mr-8 color-warn hover-bgcolor-warn" attr.aria-label="{{data?.constants?.noMsg}}" id="btn-no"
          (click)="noClicked(i,$event)" tabindex="0">{{data?.constants?.noMsg}}</button>
        <button mat-raised-button type="button" class="button-rounded color-success hover-bgcolor-success" attr.aria-label="{{data?.constants?.yesMsg}}" id="btn-yes"
          (click)="yesClicked(i,$event)" tabindex="0">{{data?.constants?.yesMsg}}</button>
        </div>
    </fieldset>
    <fieldset *ngIf="isYesClicked || isSubmitted">
      <legend tabindex="0" id="yes-clicked" class="mat-title my-16 pb-0 text-center color-success"> {{data?.constants?.thanksMsg}}</legend>
      <div *ngIf="isNoClicked && isSubmitted && extraTemplate" class="d-flex flex-ai-center">
        <ng-container *ngTemplateOutlet="extraTemplate">
        </ng-container>
      </div>
    </fieldset>
    <div class="d-flex flex-dc mt-16" *ngIf="!isSubmitted && isNoClicked">
      <h6 id="no-clicked" class="mat-body-2 mb-8 text-left" tabindex="0">{{data?.constants?.sorryMsg}}</h6>
      <form action="#" id="know-more-form" class="d-flex flex-dc m-0" *ngIf="!isSubmitted">
        <mat-form-field color="accent" appearance="fill">
          <mat-label for="knowMoreMsg">{{data?.constants?.knowMoreMsg}}</mat-label>
          <textarea matInput id="knowMoreMsg" name="moreInfo" placeholder="{{constants?.typeHere}}" maxlength="1000"
          [(ngModel)]="textValue"></textarea>
        </mat-form-field>
        <button mat-raised-button color="accent" type="submit" class="button-rounded ml-auto" (click)="submitClicked(textValue,i,$event)">{{constants?.submitButton}}</button>
      </form>
      <p class="mat-title color-accent text-center my-16" hidden="true" *ngIf="isSubmitted">{{data?.constants?.thanksMsg}}</p>
    </div>
  </div>
  </mat-expansion-panel>
</mat-accordion>
```

The appearance of the above basic Expansion Panel appears as follows.

<figure><img src="../../../../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

**Expansion Panel with Custom Styling**

We established a mixin named "**mat-expansion-panel**" in "**\_mat-expansion-panel.scss**" situated within the "**mat-themes**" folder. Subsequently, this "**\_mat-expansion-panel.scss**"  was imported into the "**includes.scss**" file.

{% code title="_mat-expansion-panel.scss" %}
```scss
@use "@angular/material"as mat;
@use "sass:map";
// @use './palette'as *;
@use './theme-palettes/index' as *;

@mixin mat-expansion-panel($theme) {
  // Get the color config from the theme.
  $color-config: mat.get-color-config($theme);
  // Get the primary color palette from the color-config.
  $primary: map.get($color-config, 'primary');
  $accent: map.get($color-config, 'accent');
  $warn: map.get($color-config, 'warn');
  $background: map.get($color-config, 'background');
  $foreground: map.get($color-config, 'foreground');

  .mat-accordion .mat-expansion-panel {
    margin-bottom: 1rem;
    box-shadow: 0.375rem 0.375rem 0.125rem 0 rgb(0 0 0 / 10%);
    .mat-expansion-panel-header-title {
      font-weight: bold;
    }
  }
  .mat-accordion .mat-expansion-panel, .mat-accordion .mat-expansion-panel:not(.mat-expanded), .mat-accordion .mat-expansion-panel:not(.mat-expansion-panel-spacing), .mat-accordion .mat-expansion-panel:first-of-type, .mat-accordion .mat-expansion-panel:last-of-type {
    border-radius: 1.5rem;
  }
  .mat-accordion .mat-expansion-panel:last-of-type {
    margin-bottom: 0;
  }

  /* For now overidding mb-0 to mb-16 for batch details */
  .mat-accordion>.mat-expansion-panel-spacing:last-child {
    margin-bottom: 1rem;
  }
  .mat-help-page{
    .mat-slide-toggle{
      width: 100%;
      .mat-slide-toggle-label{
        flex-direction: row-reverse;
        justify-content: space-between;
      }
    }
  }
}
```
{% endcode %}

{% code title="includes.scss" %}
```scss
@import './mat-expansion-panel';
```
{% endcode %}

A mixin was crafted and then imported into the "**themes.scss**" file within the "**app-themes**" section.

{% code title="themes.scss" %}
```scss
@include mat-expansion-panel($app-themes);
```
{% endcode %}

The end result will be as follows:

<figure><img src="../../../../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

Mat expansion panels provide an effective way to organize and display structured information while maintaining a clean and user-friendly interface.
