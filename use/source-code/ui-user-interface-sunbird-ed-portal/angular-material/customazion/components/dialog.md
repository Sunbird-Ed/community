# Dialog

A "[**mat-dialog**](https://v14.material.angular.io/components/dialog/overview)" is a user interface component provided by Angular Material that facilitates the creation of modal dialog boxes in web applications. Modal dialogs are typically used to display additional information, request user input, or present critical messages without navigating to a new page. Mat dialogs are often employed for tasks like form submissions, confirmations, or detailed information display. Key features and characteristics of mat dialogs include:

1. **Modal Behavior**: Mat dialogs are modal, meaning they temporarily block interaction with the underlying content until the dialog is closed, ensuring the user's focus remains on the dialog.
2. **Custom Content**: You can populate mat dialogs with custom content, including forms, messages, tables, or any other components and elements as needed for your specific use case.
3. **Actions and Buttons**: Mat dialogs often contain buttons for actions like confirmation, cancellation, or any custom action you define. These buttons can trigger specific behavior upon interaction.
4. **Theming and Styling**: Angular Material provides theming and styling options, allowing you to customize the appearance of mat dialogs to align with your application's design and branding.
5. **Accessibility**: Mat dialogs are designed with accessibility in mind, ensuring keyboard navigation and screen reader compatibility.

Mat dialogs are commonly used in various contexts, including:

* **Form Submission**: Confirming or editing form submissions before saving data.
* **Information Display**: Displaying detailed information or reports.
* **User Prompts**: Requesting user input for important actions.
* **Alerts and Notifications**: Displaying alerts, warnings, or success messages.

Here's a basic example of how you can use the mat-dialog component in an Angular Material application:

Before writing code in our HTML components, we initially imported and declared the MatChipsModule in "**material.module.ts**".

```typescript
import {MatDialogModule} from '@angular/material/dialog';

@NgModule({
  declarations: [
    PillsGridComponent,
    PillItemComponent
  ],
  imports: [
    MatDialogModule
  ],
  exports: [
    PillsGridComponent,
    PillItemComponent
  ]
})
```

{% code title="location-selection.component.html" %}
```html
<app-modal-wrapper *ngIf="showModal && !isStepper"
  [config]="{disableClose: true, width: '45rem', id: locationSelectionModalId, panelClass: ['location-selection-modal', 'material-modal']}"
  (dismiss)="closeModal()">
  <ng-template sbModalContent let-data>

    <div mat-dialog-title class="flex-jc-center flex-dc mb-0">
      <ng-content select="[slot=popup-header]"></ng-content>
      <button mat-mini-fab color="warn" class="ml-auto" aria-label="close dialog" mat-dialog-close
        *ngIf="isClosable"><mat-icon>close</mat-icon></button>
    </div>

    <mat-dialog-content class="pt-0">
      <p class="mat-subheading-2 mb-0 text-left" tabindex="0"><ng-content select="[slot=popup-sub-header]" class="mt-8"></ng-content></p>
      <div class="w-100" [appTelemetryImpression]="telemetryImpression">
        <sb-form
          *ngIf="sbFormLocationSelectionDelegate.locationFormConfig && sbFormLocationSelectionDelegate.locationFormConfig.length"
          [config]="sbFormLocationSelectionDelegate.locationFormConfig"
          (initialize)="sbFormLocationSelectionDelegate.onFormInitialize($event)"
          (valueChanges)="sbFormLocationSelectionDelegate.onFormValueChange($event)"
          (dataLoadStatus)="sbFormLocationSelectionDelegate.onDataLoadStatusChange($event)">
        </sb-form>
      </div>
    </mat-dialog-content>

    <mat-dialog-actions align="end">
      <ng-content select="[slot=popup-footer]" class="text-left mb-8" tabindex="0"></ng-content>
      <button mat-raised-button type="button" class="button-rounded text-uppercase" type="button"
        [class.sb-btn-disabled]="sbFormLocationSelectionDelegate.isLocationFormLoading"
        [disabled]="sbFormLocationSelectionDelegate.isLocationFormLoading" (click)="clearUserLocationSelections()"
        tabindex="0">{{resourceService?.frmelmnts?.btn?.clear}}
      </button>
      <button mat-raised-button color="accent" type="button" class="button-rounded text-uppercase ml-8" type="submit"
        [class.sb-btn-disabled]="sbFormLocationSelectionDelegate.isLocationFormLoading || sbFormLocationSelectionDelegate.formGroup?.invalid"
        [disabled]="sbFormLocationSelectionDelegate.isLocationFormLoading || sbFormLocationSelectionDelegate.formGroup?.invalid"
        (click)="updateUserLocation()" tabindex="0">{{resourceService?.frmelmnts?.btn?.submit}}
        <mat-icon>arrow_right_alt</mat-icon>
      </button>
    </mat-dialog-actions>

  </ng-template>
</app-modal-wrapper>
```
{% endcode %}

The appearance of the above basic dialog appears as follows.

<figure><img src="../../../../../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

**Dialog with Custom Styling**

We established a mixin named "**theme-mat-modal**" in "**\_mat-dialog.scss**" situated within the "**mat-themes**" folder. Subsequently, this "**\_mat-dialog.scss**"  was imported into the "**includes.scss**" file.

{% code title="_mat-dialog.scss" %}
```scss
@use "@angular/material"as mat;
@use 'sass:map';

@mixin theme-mat-modal($theme) {
  // Get the color config from the theme.
  $color-config: mat.get-color-config($theme);
  // Get the primary color palette from the color-config.
  $primary: map.get($color-config, 'primary');
  $accent: map.get($color-config, 'accent');
  $warn: map.get($color-config, 'warn');
  $background: map.get($color-config, 'background');

  .cdk-overlay-pane.fullscreen-modal {
    width: 100% !important;
    max-width: 100% !important;
  }

  .mat-dialog-container {
    position: relative;
    padding: 0;
    background-color: var(--sbt-body-bg);
    border-radius: 1.5rem;
  }

  .mat-dialog-title {
    // background-color: mat.get-color-from-palette($primary, 500);
    color: mat.get-color-from-palette($accent);
    margin: 0;
    padding: 1rem 1rem;
    display: flex;
    align-items: center;

    h2 {
      margin-bottom: 0 !important;
    }
  }
  .mat-dialog-content {
    padding: 1rem;
    margin: 0;
    text-align: left;
    ::ng-deep html[dir="rtl"]{
      text-align: right;
      text-align: unset;
    }
  }
  .mat-dialog-actions {
    padding: 1rem 1rem;
    margin: 0;
  }
}
```
{% endcode %}

{% code title="includes.scss" %}
```scss
@import './mat-dialog';
```
{% endcode %}

A mixin was crafted and then imported into the "**themes.scss**" file within the "**app-themes**" section.

{% code title="themes.scss" %}
```scss
 @include theme-mat-modal($theme);
```
{% endcode %}

The end result will be as follows:

<figure><img src="../../../../../../.gitbook/assets/image (67).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../../../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>
