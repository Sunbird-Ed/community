# Card

A "[**mat-card**](https://v14.material.angular.io/components/card/overview)" is a component provided by Angular Material, primarily used for creating structured and visually appealing containers to display content or information. These cards are commonly employed in web applications to present various types of data, such as text, images, buttons, and other interactive elements, in an organized and consistent manner.

{% hint style="info" %}
We've already explored the usage of a basic mat card in the previous section on [**component usage**](../../../../../developer-guide/ui-user-interface-sunbird-ed-portal/angular-material/components-usage.md).
{% endhint %}

This section will guide you through the process of customizing the card.

The following code represents a basic card created using the Angular Material card component.

```html
<mat-card role="link" tabindex="0" layout=""
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

The expected output is as follows:

<figure><img src="../../../../../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

### Customize and Style

For customizing and styling Angular Material components in your Angular application, you can leverage different methods. These encompass CSS, Angular Material theming, and specific customization options for each component.

The customization for the earlier basic code has been applied through the CSS/SCSS located in the **\_mat-card.scss** file within the **mat-themes** folder. In the above HTML file, it's necessary to include the "layout" attribute.

<pre class="language-html"><code class="lang-html">&#x3C;mat-card role="link" tabindex="0" layout="v2-type1"> 
<strong>    &#x3C;!-- card items go here -->
</strong>&#x3C;/mat-card>
</code></pre>

```scss
[layout='v2-type1'] {
  .mat-card {
    width: 100%;
    display: flex;
    flex-direction: column;
    z-index: 2;
    overflow: hidden;
    position: relative;
    border-radius: 1rem;
    box-shadow: var(--sbt-box-shadow-6px) !important;
    padding: 0;
    .mat-card-header {
      border-radius: 1rem 1rem 0 0;
      order: 2;
      z-index: 2;
      padding-top: 2rem;
      display: block;
      margin-top: 3rem;
      .mat-card-avatar {
        height: 4rem;
        width: 4rem;
        justify-content: center;
        border-radius: 50%;
        position: absolute;
        top: 0.75rem;
        z-index: 1;
        left: 1rem;
        border: 0.1875rem solid var(--white);
      }
    }
    .mat-card-banner img {
      position: absolute;
      top: -2.25rem;
      left: 0;
      max-width: 100%;
      z-index: 1;
      order: 1;
      width: 100% !important;
      margin: 0;
    }
    .mat-card-content {
      padding: 0 1rem;
      margin-top: 0.25rem;
      margin-bottom: 0.5rem !important;
      order: 3;
      &>:first-child {
        min-height: 3.5rem;
      }
    }
    .mat-card__type {
      top: 1rem;
      right: 0.5em;
      ::ng-deep html[dir="rtl"] & {
        left: 0.5em;
        right: unset;
      }
      border-radius: 1.5rem;
      z-index: 2;
      bottom: unset !important;
      &::before {
        content: none !important;
      }
    }
    .mat-card-svg-tail {
      display: none;
    }
  }
}
```

Applying the above-mentioned CSS/SCSS code to the basic structure will result in the customized card as follows:

<figure><img src="../../../../../../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

Another example of a customized card code is written below.

```scss
[layout='v2-type2'] {
  .mat-card {
    display: flex;
    border-radius: 1rem;
    box-shadow: 0.375rem 0.375rem 0.125rem 0 var(--sbt-box-shadow-black) !important;
    padding: 0rem;
    height: 100%;
    min-height: 12rem;
    .mat-card-header {
      width: 40%;
      margin-bottom: 0 !important;
      .mat-card-avatar {
        height: 100%;
        width: 100%;
        border-radius: 1rem 0 0 1rem;
      }
      .mat-card-header-text {
        position: absolute;
        left: 40%;
        width: 60%;
        padding: 1rem;
        margin: 0;
        top: 0;
      }
    }
    .mat-card-content {
      width: 60%;
      padding: 3.75rem 1rem 1rem 1rem;
      margin: 0;
      .text-left {
        position: absolute;
        bottom: 0.5rem;
      }
    }
    .mat-card__type {
      margin: 0 !important;
      border-radius: 0 0.5rem 0.5rem 0;
      top: 1rem;
      left: 0;
      ::ng-deep html[dir="rtl"] & {
        right: 0;
        left: unset;
      }
      text-align: center;
      bottom: unset !important;
      &::before {
        content: none !important;
      }
    }
    .mat-card-banner img,
    .mat-card-svg-tail {
      display: none;
    }
  }
}
```

And the expected output is:

<figure><img src="../../../../../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

In a similar way, we can customize our card using various styles.

Remember to check the official [**Angular Material Card documentation**](https://v14.material.angular.io/components/card/overview) for the latest features and detailed information.
