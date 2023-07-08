# The first part
![IMG_0266](https://github.com/S-way520/Sin-xy-RealityKit-SwiftUI/assets/95877651/d297a9c4-a5f0-4a01-bd7f-62ea85a4e96d)
# The second part
Code file 1
```swift
import SwiftUI
@main
struct MyApp: App {
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
}
```
Code file 2
```swift
import SwiftUI
import RealityKit
struct ContentView: View {
    var body: some View {
        ARViewContainer().edgesIgnoringSafeArea(.all)
    }
}
struct ARViewContainer: UIViewRepresentable {
    func makeUIView(context: Context) -> ARView {
        let arView = ARView(frame: .zero)
        let anchorEntity = AnchorEntity(plane: .horizontal)
        let sphereRadius: Float = 0.01
        let gridSize = 30
        let spacing: Float = 1 / 5
        for siny in 0..<gridSize {
            for sinx in 0..<gridSize {
                let sphereMesh = MeshResource.generateSphere(radius: sphereRadius)
                let sphereMaterial = SimpleMaterial(color: .red, isMetallic: false)
                let sphereEntity = ModelEntity(mesh: sphereMesh, materials: [sphereMaterial])
                let x = Float(sinx) * spacing - (Float(gridSize) / 2) * spacing
                let y = Float(siny) * spacing - (Float(gridSize) / 2) * spacing
                let sinX = sin(x)
                let sinY = sin(y)
                let z = sinX * sinY
                let transform = Transform(translation: SIMD3<Float>(x, z, y) / 10)
                sphereEntity.transform = transform
                anchorEntity.addChild(sphereEntity)
                arView.scene.addAnchor(anchorEntity)
            }
        }
        return arView
    }
    func updateUIView(_ uiView: ARView, context: Context) {}
}
```
