# Card

A "[**mat-card**](https://v14.material.angular.io/components/card/overview)" is a component provided by Angular Material, primarily used for creating structured and visually appealing containers to display content or information. These cards are commonly employed in web applications to present various types of data, such as text, images, buttons, and other interactive elements, in an organized and consistent manner.

Key features of mat cards typically include:

1. **Card Structure**: Mat cards have a card-like structure, often with rounded corners, creating a visually distinct and organized presentation of content.
2. **Content Containers**: These cards can house a variety of content, such as text, images, icons, buttons, and other Angular Material components, making them versatile for displaying different types of information.
3. **Header and Footer**: Mat cards often come with header and footer sections where you can add titles, subtitles, action buttons, or any other relevant content to the card.
4. **Elevation and Shadow**: Mat cards typically have subtle elevation and shadow effects, giving them a tactile appearance and making them stand out from the background.
5. **Interactive Elements**: You can include interactive elements within mat cards, such as buttons, links, or form controls, allowing users to interact with or take actions related to the card's content.
6. **Custom Styling**: Angular Material provides theming and styling options to customize the appearance of mat cards to match your application's design and branding.

{% hint style="info" %}
We've previously covered the utilization of a fundamental mat card in the [**component usage**](../../../../developer-guide/ui-user-interface-sunbird-ed-portal/angular-material/components-usage.md) and also explore the process of customizing the card within the [**Card**](../customazion/components/card.md)**.**
{% endhint %}

We imported card module in **card.module.ts**

{% code title="card.module.ts" %}
```typescript
import {MatCardModule} from '@angular/material/card';

 imports: [
    CommonModule,
    MatCardModule
  ]
```
{% endcode %}

We have added card related code in **library-card-v2.component.html**

{% code title="library-card-v2.component.html" %}
```html
<mat-card role="link" tabindex="0"
[ngClass]="{'recently-viewed': type === LibraryCardTypes.RECENTLY_VIEWED, 'offline': isOffline, 'selected': isSelected}" (click)="onClick($event)" *ngIf="!isLoading">
  <mat-card-header>
    <div mat-card-avatar> <img [src]="cardImg" alt=""></div>
    <mat-card-title class="sb__ellipsis sb__ellipsis--two text-left">{{content?.name}}</mat-card-title>
    <a *ngIf="isMenu" role="button" aria-label="View more actions menu" class="menu" (click)="onMenuClick($event);$event.stopPropagation()"></a>
  </mat-card-header>
  <div class="mat-card-banner">
    <img mat-card-image [src]="svgToDisplay" alt=""/>
  </div>
  <mat-card-content>
    <!-- card mobile view details -->
   <div class="d-flex flex-w-wrap mat-card-chips-list">
    <mat-chip-list aria-label="data selection" *ngIf="content?.organisation && content?.organisation.length > 0" tabindex="-1">
      <mat-chip class="data_0">{{content?.organisation[0]}}</mat-chip>
      <mat-chip class="data_0" *ngIf="content?.organisation.length > 1">+{{content?.organisation.length-1}}</mat-chip>
    </mat-chip-list>
    <mat-chip-list aria-label="data selection" *ngIf="content?.medium && content?.medium.length > 0">
      <mat-chip class="data_1">{{content?.medium[0]}}</mat-chip>
      <mat-chip class="data_1" *ngIf="content?.medium.length > 1">+{{content?.medium.length-1}}</mat-chip>
    </mat-chip-list>
    <mat-chip-list aria-label="data selection" *ngIf="content?.gradeLevel && content?.gradeLevel.length > 0">
      <mat-chip class="data_2">{{content?.gradeLevel[0]}}</mat-chip>
      <mat-chip class="data_2" *ngIf="content?.gradeLevel.length > 1">+{{content?.gradeLevel.length-1}}</mat-chip>
    </mat-chip-list>
   </div>
   <!-- content for only desktop -->
   <div *ngIf="type === LibraryCardTypes.DESKTOP_TEXTBOOK || type === LibraryCardTypes.PORTAL_QRCODE_FLATRESULT">
    <div class="d-flex flex-ai-center flex-jc-space-between mat-card-info">
      <!-- other meta info subject, publisher/organizer etc -->
      <div class="text-left mat-small">
        <ng-container *ngIf="content?.subject && content?.subject.length > 0">
          <div class="sb__ellipsis">
            <span>Subject: </span> <span>{{content?.subject[0]}}</span> <span class="mr-8" *ngIf="content?.subject.length > 1"> +{{content?.subject.length-1}}
            </span>
          </div>
        </ng-container>
        <ng-container *ngIf="content?.organisation && content?.organisation.length > 0">
          <div class="sb__ellipsis">
            <span>Publisher: </span> <span>{{content?.organisation[0]}}</span>
            <span class="mr-8" *ngIf="content?.organisation.length > 1"> +{{content?.organisation.length-1}}
            </span>
          </div>
        </ng-container>
      </div>
      <!-- other meta info Badge and card category Book, learn, practice -->
      <div class="mat-card__badge mr-16" *ngIf="content?.badgeAssertions">
        <img [src]="content?.badgeAssertions[0]?.badgeClassImage" alt="" />
      </div>
    </div>
    <div *ngIf="type === LibraryCardTypes.PORTAL_QRCODE_FLATRESULT">
      <button mat-raised-button color="accent" class="w-100 button-label">
        <mat-icon class="mr-4">play_circle</mat-icon>
        {{btnlabel}}
      </button>
    </div>
  </div>
  <!-- Qr code card -->
  <div *ngIf="type === LibraryCardTypes.QRCODE_RESULT">
    <!-- Section area if not available it will be hidden -->
    <div class="text-left mat-small" *ngIf="section !== null">
      <div class="sb__ellipsis" *ngIf="section">
        <span class="label">moreInfoLabel: </span>
        <span class="value">section</span>
      </div>
    </div>
  </div>
  <ng-container
    *ngTemplateOutlet="gridTemplate; context: {$implicit: content?.hoverData, hoverData: content?.hoverData, content:content}"
    class="card-hover">
  </ng-container>
  <div class="mat-card__type px-8 d-flex flex-ai-center flex-jc-center" *ngIf="content?.primaryCategory || content?.contentType">
    <span class="sb__ellipsis">{{content?.primaryCategory || content?.contentType}}</span>
  </div>
  <svg width="79px" class="mat-card-svg-tail" align="end" height="36px" viewBox="0 0 79 36" version="1.1"
    xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
    <g stroke="none" stroke-width="1" fill="none" fill-rule="evenodd">
      <g transform="translate(-735.000000, -524.000000)" class="svg-tail__rc">
        <g transform="translate(517.000000, 338.000000)">
          <g>
            <path
              d="M224.269945,224.907985 C224.269945,224.907985 217.096964,205.264724 219.487958,199.23369 C221.878951,193.203161 229.905965,205.609232 231.442925,210.261729 C231.442925,210.261729 230.930605,187 237.762123,187 C244.59339,187 245.447423,217.498667 245.447423,217.498667 C245.447423,217.498667 247.838417,203.54168 252.27894,203.54168 C256.719214,203.54168 251.424907,219.049331 253.645044,218.704823 C255.865431,218.360315 264.612662,211.290301 270.931859,218.871747 C277.250806,226.453445 274.347493,238.1705 281.17901,237.998119 C288.010277,237.825992 268.503575,211.123125 272.431528,205.95374 C276.359732,200.784607 286.265169,212.84617 287.119203,215.94775 C287.119203,215.94775 286.606883,199.23369 291.218013,199.23369 C295.829393,199.23369 296,223.18494 296,223.18494 L224.269945,224.907985 Z">
            </path>
          </g>
        </g>
      </g>
    </g>
  </svg>
  </mat-card-content>
</mat-card>
```
{% endcode %}

We established a mixin named "**theme-mat-card**" in "**\_mat-card.scss**" situated within the "**mat-themes**" folder. Subsequently, this "**\_mat-card.scss**"  was imported into the "**includes.scss**" file.

{% code title="_mat-card.scss" %}
```scss
@use "@angular/material" as mat;
@use 'sass:map';
@use './theme-palettes/index' as *;
// @use './palette' as *;

@mixin theme-mat-card($theme) {
  // Get the color config from the theme.
  $color-config: mat.get-color-config($theme);
  // Get the primary color palette from the color-config.
  $primary: map.get($color-config, 'primary');
  $accent: map.get($color-config, 'accent');
  $warn: map.get($color-config, 'warn');
  $background: map.get($color-config, 'background');

  $color-accent: mat.get-color-from-palette($accent);
  $color-accent-100: mat.get-color-from-palette($accent, 100);
  --cc-mat-card-title:#{$color-accent};
  --cc-mat-card-svg-flower:#{$color-accent};
  --cc-mat-card-selected-border:#{$color-accent};
  --cc-mat-card-selected-bg:#{$color-accent-100};
  .mat-card-title {
    color: mat.get-color-from-palette($accent);
  }
  .mat-card-svg-tail{
    .svg-tail__rc{
      stroke: var(--cc-mat-card-svg-flower);
    }
  }
  .mat-card .mat-chip-list-wrapper {
    justify-content: flex-start;
    margin: 0;
  }
  .cardSlick .mat-card {
    width: 20rem;
  }
  .mat-card-header-text {
    overflow: hidden;
  }
  .mat-card.member-card:hover {
    background-color: mat.get-color-from-palette($accent, 500) !important;
    color: mat.get-color-from-palette($accent, 500-contrast);
  }
}
[layout='v2-type4'] {
 .mat-card{
    cursor: pointer;
    position: relative;
    border-radius: 1.5rem;
    box-shadow: var(--sbt-box-shadow-6px) !important;
    overflow: hidden;
    width: 100%;
    height: 100%;
    display: flex;
    padding: 0;
    flex-direction: column;
    .mat-card-header {
      display: block;
      z-index: 2;
      order: 2;
      width: 100%;
      justify-content: space-between;
      padding: 0 1rem;
      margin-bottom: 0 !important;
      .mat-card-avatar {
        width: 4.5rem;
        height: 4.5rem;
        border-radius: 50%;
        position: absolute;
        top: 3rem;
        right: 2rem;
        border: 0.1875rem solid var(--cc-mat-card-avatar-border);
        z-index: 1;
        img {
          position: absolute;
          left: 50%;
          top: 50%;
          transform: translate(-50%,-50%);
        }
        html[dir='rtl'] & {
          right: auto;
          left: 2rem;
        }
      }
      .mat-card-header-text{
        margin: 0;
        width: 100%;
      }
      .mat-card-title{
        width: 70%;
      }
    }
    .mat-card-banner{
      height: 4.5rem;
      border-radius: 1rem;
      overflow: hidden;
      margin: 1rem;
      img{
        width: 100%;
        height: 100%;
        object-fit: cover;
        margin: 0;
      }
    }
    .mat-card-content {
      order: 3;
      margin: 0 !important;
    }
    .mat-card-info{
      padding: 0 1rem 1rem;
    }
    .mat-card-chips-list{
      padding: 0 1rem;
    }
    .mat-card__type {
      top: 2.625rem;
      left: 0;
      margin: 0 !important;
      html[dir='rtl'] & {
        right: 0;
        left: unset;
      }
      &::before {
        left: auto !important;
        html[dir='rtl'] & {
          left: -0.5rem !important;
          transform: rotatex(180deg);
          right: unset;
        }
      }
    }
    &.selected{
      border-radius: 1.5rem;
    }
    &.recently-viewed{
      .mat-card-header .mat-card-avatar{
        height: 5.5rem;
        width: 5.5rem;
        right: 2.5rem;
      }
    }
    &:hover{
      transform: translate(0);
      box-shadow: 0 0.125rem 0.4375rem 0 rgba(var(--rc-rgba-black),.16) !important;
    }
  }
}
```
{% endcode %}

{% code title="includes.scss" %}
```scss
@import './mat-card';
```
{% endcode %}

A mixin was crafted and then imported into the "**themes.scss**" file within the "**app-themes**" section.

{% code title="themes.scss" %}
```scss
@include theme-mat-card($app-themes);
```
{% endcode %}

The end result will be as follows:

<figure><img src="../../../../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>
