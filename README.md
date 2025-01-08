
[![AGM - Angular Google Maps](assets/images/angular-google-maps-logo.png)](https://github.com/mehulk05/ng-angular-maps/)

# AGM - Angular Google Maps (Updated)

This is a fork of the original `AGM - Angular Google Maps` library with support for the latest Angular versions. This repository provides Angular components for Google Maps, maintaining the functionality of the original library while extending compatibility.

### What's New?
1. **Angular 12+ Support**: Full compatibility with Angular versions 12 and above.
2. **Bug Fixes**: Resolved several issues from previous releases.
3. **Performance Enhancements**: Optimized for better performance in modern Angular applications.

---

## Supported Angular Versions

| Angular Version Range | Supported by AGM v1.0.0 |
| --------------------- | ----------------------- |
| 12.x.x                | Yes                     |
| 13.x.x                | Yes                     |
| 14.x.x                | Yes                     |
| 15.x.x                | Yes                     |
| 16.x.x                | Yes                     |
| 17.x.x                | Yes                     |
| 18.x.x                | Yes                     |
| Latest (currently 19.x) | Yes                     |

ng-agm-core-lib v1.0.0 supports all Angular versions from 12.x to the latest (currently 19.x).  
> **Note:** ng-agm-core-lib v1.0.0 will continue to support future Angular versions as well, ensuring compatibility with the latest updates and features.

---

## Packages

| Package                  | Downloads                                                                                                                                         |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| ng-agm-core-lib          | [![ng-agm-core-lib](https://img.shields.io/npm/dm/ng-agm-core-lib.svg)](https://www.npmjs.com/package/ng-agm-core-lib)                             |

---

## Playing with AGM (Angular Google Maps)

If you just want to play with AGM and don't want to set up a full project, you can use the following Plunker. It has all the dependencies to play with Angular, TypeScript, and of course `AGM`:

[&raquo; Play with Angular Google Maps on Stackblitz](https://stackblitz.com/edit/angular-google-maps-demo)

---

# How to Use AGM - Angular Google Maps

---

## Table of Contents

1. [Installation](#installation)
2. [Setup and Configuration](#setup-and-configuration)
3. [Usage Example](#usage-example)
4. [Supported Versions](#supported-versions)
5. [API Reference](#api-reference)
6. [Note](#note)

---

## Installation

To install the `ng-agm-core-lib` package, run the following command in your Angular project directory:

```bash
npm install ng-agm-core-lib
```

---

## Setup and Configuration

1. **Import the AGM Core Module**  
After installation, import `AgmCoreModule` into your `AppModule` (or another module that requires the map functionality). You also need to provide your Google Maps API key as follows:

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { FormsModule } from '@angular/forms';
import { AgmCoreModule } from 'ng-agm-core-lib';

@NgModule({
  imports: [
    BrowserModule,
    FormsModule,
    AgmCoreModule.forRoot({
      apiKey: 'YOUR_GOOGLE_MAPS_API_KEY'
    })
  ],
  declarations: [AppComponent],
  bootstrap: [AppComponent]
})
export class AppModule {}
```

> **Note:** Replace `'YOUR_GOOGLE_MAPS_API_KEY'` with your actual Google Maps API key. You can obtain it from the [Google Cloud Console](https://console.cloud.google.com/).

---

## Usage Example

Here's a basic usage example to display a map with markers and circles:

```html
<h1>Angular Google Maps (AGM) Demo</h1>
<p><a href="https://angular-maps.com/" target="_blank">Official Website</a></p>

<agm-map 
  [latitude]="lat"
  [longitude]="lng"
  [zoom]="zoom"
  [disableDefaultUI]="false"
  [zoomControl]="false"
  (mapClick)="mapClicked($event)">

  <agm-marker 
      *ngFor="let m of markers; let i = index"
      (markerClick)="clickedMarker(m.label, i)"
      [latitude]="m.lat"
      [longitude]="m.lng"
      [label]="m.label"
      [markerDraggable]="m.draggable"
      (dragEnd)="markerDragEnd(m, $event)">
      
    <agm-info-window>
      <strong>InfoWindow content</strong>
    </agm-info-window>
    
  </agm-marker>
  
  <agm-circle [latitude]="lat + 0.3" [longitude]="lng" 
      [radius]="5000"
      [fillColor]="'red'"
      [circleDraggable]="true"
      [editable]="true">
  </agm-circle>

</agm-map>
```

```typescript
import { Component } from '@angular/core';
import { MouseEvent } from '@agm/core';

@Component({
  selector: 'my-app',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  // google maps zoom level
  zoom: number = 8;
  
  // initial center position for the map
  lat: number = 51.673858;
  lng: number = 7.815982;

  clickedMarker(label: string, index: number) {
    console.log(`clicked the marker: ${label || index}`)
  }
  
  mapClicked($event: MouseEvent) {
    this.markers.push({
      lat: $event.coords.lat,
      lng: $event.coords.lng,
      draggable: true
    });
  }
  
  markerDragEnd(m: marker, $event: MouseEvent) {
    console.log('dragEnd', m, $event);
  }
  
  markers: marker[] = [
    {
      lat: 51.673858,
      lng: 7.815982,
      label: 'A',
      draggable: true
    },
    {
      lat: 51.373858,
      lng: 7.215982,
      label: 'B',
      draggable: false
    },
    {
      lat: 51.723858,
      lng: 7.895982,
      label: 'C',
      draggable: true
    }
  ];
}

// just an interface for type safety.
interface marker {
  lat: number;
  lng: number;
  label?: string;
  draggable: boolean;
}
```

---

## Note

ng-agm-core-lib v1.0.0 supports Angular 12+ and will continue to support future versions, ensuring compatibility with the latest updates and features.
