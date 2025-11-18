# City Map/UrbanMap

A OSM client specialised on urban exploration and navigation.

## The Problem

Right now, if you are searching for features like water fountains, it’s difficult to find them. Just searching for the term leads to POIs with the name “Water Fountain”.

## The Solution-Idea

A solution might be to provide easilly queryable searches for features. The only solution to actually search for features that I found was [this](https://overpass-turbo.eu/?key=amenity&value=drinking_water&template=key-value#). That’s obviously … not ideal. And even worse on mobile and on the go, when you might actually need this.

[MapLibreSwiftUI](https://github.com/maplibre/swiftui-dsl) might offer a foundation to interact with OSM as well as offer usual ways to style the maps.
