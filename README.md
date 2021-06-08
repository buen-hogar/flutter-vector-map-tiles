# vector_map_tiles

A plugin for [`flutter_map`](https://pub.dev/packages/flutter_map) that enables the use of vector tiles.

## Usage

```dart
class _MyHomePageState extends State<MyHomePage> {
  // provide a map theme
  final theme = ProvidedThemes.lightTheme();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          title: Text(widget.title),
        ),
        body: SafeArea(
            child: Column(children: [
          Flexible(
              child: FlutterMap(
            options: MapOptions(
                center: LatLng(49.246292, -123.116226),
                zoom: 10,
                maxZoom: 18,
                interactiveFlags: InteractiveFlag.doubleTapZoom |
                    InteractiveFlag.drag |
                    InteractiveFlag.pinchZoom |
                    InteractiveFlag.pinchMove,
                plugins: [VectorMapTilesPlugin()]), // be sure to register the plugin
            layers: <LayerOptions>[
              // normally you would see TileLayerOptions which provides raster tiles
              // instead this vector tile layer replaces the standard tile layer
              VectorTileLayerOptions(
                  theme: theme,
                  tileProvider: MemoryCacheVectorTileProvider(
                      delegate: NetworkVectorTileProvider(
                          urlTemplate:
                              'https://tiles.stadiamaps.com/data/openmaptiles/{z}/{x}/{y}.pbf?api_key=$apiKey',
                        // this is the maximum zoom of the provider, not the
                        // maximum of the map. vector tiles are rendered
                        // to larger sizes to support higher zoom levels
                          maximumZoom: 14),
                      maxSizeBytes: 1024 * 1024 * 2)),
            ],
          ))
        ])));
  }
}
```

See the [example](example) for details.

## Status

This plugin is in its very early stages, and is not ready for production use.

Outstanding issues:

* performance
* smooth scrolling/zooming
* transition between zoom levels when tiles are not cached
* the unknown unknowns

## License

Copyright 2021 David Green

Redistribution and use in source and binary forms, with or without modification,
are permitted provided that the following conditions are met:

1. Redistributions of source code must retain the above copyright notice,
   this list of conditions and the following disclaimer.

2. Redistributions in binary form must reproduce the above copyright notice, 
   this list of conditions and the following disclaimer in the documentation
   and/or other materials provided with the distribution.

3. Neither the name of the copyright holder nor the names of its contributors
   may be used to endorse or promote products derived from this software without
   specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY
EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES
OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT
SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT,
INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED
TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR 
BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, 
STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT
 OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.