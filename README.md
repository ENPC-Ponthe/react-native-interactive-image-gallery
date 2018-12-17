# react-native-interactive-image-gallery

This is a fork from  [InterfaceKit/react-native-interactive-image-gallery](https://github.com/InterfaceKit/react-native-interactive-image-gallery)

This module exports `ImageListContainer` and add an optional centered overlay text on each image.

Minimal example code (the original lib uses React Context that must be passed to `ImageListContainer`) :

```
import {ImageListContainer, ImageSource} from 'react-native-interactive-image-gallery'
import React, {PureComponent} from 'react';

class Galleries extends PureComponent<Props> {
    static childContextTypes = {
        onSourceContext: PropTypes.func.isRequired
    }

    constructor(props) {
        super(props)

        this._imageMeasurers = {}
        this._imageSizeMeasurers = {}
    }

    getChildContext() {
        return { onSourceContext: this._onSourceContext }
    }

    _onSourceContext = (
        imageId: string,
        cellMeasurer: Function,
        imageMeasurer: Function
    ) => {
        this._imageMeasurers[imageId] = cellMeasurer
        this._imageSizeMeasurers[imageId] = imageMeasurer
    }

    render() {
        const imageURLs: Array<ImageSource> = this.props.images.map(
            (img: Object, index: number) => ({
                URI: img.uri,
                thumbnail: img.thumbnail,
                id: img.id,
                overlayText: img.name,
            })
        )

        const { navigate } = this.props.navigation
        return <ImageListContainer images={imageURLs}
                                   onPressImage={(imageId) => doSomethingLikeNavigating(imageId))}
                                   displayImageViewer={false}
                                   topMargin={0} />
    }
}
```