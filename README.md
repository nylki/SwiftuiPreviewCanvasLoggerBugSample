# SwiftuiPreviewCanvasLoggerBugSample
Minimal reproducable sample project that triggers a a bug with the XCode Preview Canvas with Swift-6 language mode

Ticket number (Apple): `FB16918422`


```swift

import SwiftUI
import os.log

/// It appears like this only happens **with Swift 6 language mode**

struct ContentView: View {
    var body: some View {
        Text("Hello, world!")
            .padding()
        .task {
            loadData()
        }
    }
    
    private func loadData() {
        let logger = Logger()
        
        // The following line causes the compiler to crash in the XCode (Version 16.3 (16E137)) Preview Canvas:
        // "Compiling failed: argument must be a string interpolation".
        // If you comment the logger line, the Preview Canvas works.
        logger.debug("this does crash the canvas with Swift-6 language mode")
        
        
        // Also, when logging the same string wrapped a template string pattern, the canvas renders the preview just fine:
        
        // logger.debug("\("this works with Swift-6 language mode")")
        // logger.debug("this also works\(0)")
    }
}

#Preview {
    ContentView()
}


```
