# Explore the USD ecosystem

Discover the latest updates to Universal Scene Description (USD) on Apple platforms and learn how you can deliver great 3D content for your apps, games, and websites. Get to know USD for visionOS, explore MaterialX shaders and color management, and find out about some of the other improvements to the USD ecosystem.

@Metadata {
   @TitleHeading("WWDC23")
   @PageKind(sampleCode)
   @CallToAction(url: "https://developer.apple.com/wwdc23/10086", purpose: link, label: "Watch Video (14 min)")

   @Contributors {
      @GitHubUser(multitudes)
   }
}



Apple has been building on the foundation based on the new key technologies that power the 3D creative industry worldwide.

![USD and MaterialX][intro1]

[intro1]: WWDC23-10086-intro1

The first of these technologies is Universal Scene Description, or USD for short.  
It allows for a standard form of representing 3D content to share between applications.  
Now introducing support for MaterialX on xrOS to portably represent the visual appearance of objects.


## OpenUSD
- Created by Pixar. USD is an open source project, created by Pixar, recently renamed to OpenUSD.  
- Production proven and scalable, `from creators making single assets to large studios working on AAA games and films. 
- Expressive composition. USD allows for expressing of complex and flexible relationships between asset data via composition.  
- On Apple platforms since 2017. Apple was an early adopter of USD, adding it to our platforms in 2017 and growing support since.  
- Heart of 3D content on XrOS. Today, USD is at the heart of 3D Content on xrOS.

## MaterialX
- MaterialX is also an open source project, created at Industrial Light & Magic for their work on Star Wars, now developed in conjunction with others like Autodesk and adopted by the Academy Software Foundation.  
- Code-free shaders. It allows artists to combine shader logic into a node graph within their 3D applications, all without needing to know how to code.  
- Embedded in USD. This graph can also be embedded inside USD, so it travels with the scene data.  
- Supported on xrOS. Apple is supporting MaterialX first on xrOS with RealityKit, Apple's real-time 3D rendering framework for building immersive spatial experiences.

Four areas to cover:

- 3D content in Apple apps
- MaterialX
- Color management
- New in USD

# 3D content in Apple apps

Now Quick Look is available to xrOS.

There is a great talk on how to easily author content that will look great on xrOS.

![3D content in Apple apps][content1]

[content1]: WWDC23-10086-content1

Freeform, introduced last year is a powerful and easy-to-use brainstorming app. Freeform now gives the ability to embed USDZ content, and now collaborate on 3D assets is possible across all supported platforms like macOS, iOS, iPadOS, and now xrOS.

![USD and MaterialX][content2]

[content2]: WWDC23-10086-content2

Safari also introduces new support for 3D Content with the Model element. The Model element is available on all Apple platforms with Safari and can be enabled under the Developer menu on macOS or Settings on other platforms. 

The Model element is embedding a USDZ file into the web page with an interactive view, with the ability to rotate around objects.

This allows creation of more interactive websites, and apple is working with the W3C Immersive Web Working Group on standardization.

![USD and MaterialX][content3]

[content3]: WWDC23-10086-content3

We also have Reality Composer Pro, a new macOS application joining our suite of tools for creators and developers. Using USD's composition features, it lets multiple people work in parallel, enabling each person to tackle a different aspect of the scene and see them combined together as each asset updates.

![USD and MaterialX][content4]

[content4]: WWDC23-10086-content4

Assets can be authored to USD in your own content creation applications, and Reality Composer Pro lets us prepare them for use in xrOS apps and experiences.

Check out the Reality Composer Pro sessions to learn more:

[Explore materials in Reality Composer Pro - WWDC23](https://developer.apple.com/videos/play/wwdc2023/10164)

# MaterialX
As important as the 3D models are the shaders and materials that give them the individual visual aesthetic.

MaterialX allows to have bespoke visuals that can be transported inside the USD scenes into RealityKit applications on xrOS. Reality Composer Pro introduces a Shader Graph that authors MaterialX nodes embedded inside of USD files.

![USD and MaterialX][content5]

[content5]: WWDC23-10086-content5

This enables the creation of shaders using an interactive node graph to compose the shader logic. MaterialX shader graphs are how creators will be constructing custom shaders for xrOS content. In addition to many of the standard MaterialX nodes, Reality Composer Pro also has a few custom MaterialX nodes that enable a range of xrOS-specific platform features.

## Custom Material nodes

![USD and MaterialX][content6]

[content6]: WWDC23-10086-content6

Some of these shader nodes are: RealityKit PBR, physically based rendering shader which enables realistic-looking 3D content; RealityKit Unlit, an unlit shader that do more stylized shading; Geometry Modifiers that allow to modify surface deformations; as well as several custom utility nodes.

There is a great developer session on how to use the Shader Graph:

[Explore materials in Reality Composer Pro - WWDC23](https://developer.apple.com/videos/play/wwdc2023/10164)  

Support for MaterialX with USD grows across established third-party 3D applications, like SideFX's Houdini and LookdevX in Autodesk's Maya, shown here.

![USD and MaterialX][content7]

[content7]: WWDC23-10086-content7

Reality Composer Pro then lets preview the shaders to see how they'll look before deployment to device.

## Metal in MaterialX

- Open source tooling
- Metal shader code generation
- Available in Material 1.38.7
- Material in USD on macOS

MaterialX is an open source project which enables creators and developers to make use of it in their own workflows and applications directly.

The MaterialX project includes support for generating shader code from your MaterialX node graphs.

Apple has added support to the project for creating Metal shader code to make the most use of our powerful GPUs.

This is now available in the MaterialX 1.38.7 release.

For developers who use USD, this also enables the future use of MaterialX within USD on macOS.

## What is a color space
- Range and properties of color
- Display P3

Having confidence in how shaders behave is important, but so is having confidence in what the colors look like.

The handling of color space management for RealityKithas been expanded, to make accurate-looking 3D content capable of using a wide gamut color range.

Color spaces are how graphics programs understand how to represent colors from digital values, including the range of colors available. This allows multiple applications to reliably display and edit the same colors.

Apple displays primarily use Display P3 as their color space, whereas many other platforms may use the more commonplace sRGB. DisplayP3 marries the wider primary range of digital cinema with the sRGB gamma curves used by computer displays.

In fact, it's capable of displaying up to 25 percent more colors than traditional sRGB, shown here as the black line within the greater Display P3 color space.

![USD and MaterialX][content8]

[content8]: WWDC23-10086-content8

This allows for representing more of the colors we see in the real world. Most color and image workflows tend to use sRGB, which represents a standard range of colors used by many monitors for decades.

```swift
// sRGB
asset inputs:file = @0/texture.png@
```

These are still capable of creating good-looking content, but can't take full advantage of the beautiful, wider-range displays that Apple products ship with.

``` swift
// Display P3
asset inputs:file = 00/texture.png@ (
colorSpace = "srgb_displayp3"
)
```

![USD and MaterialX][content9]

[content9]: WWDC23-10086-content9

Textures authored with Display P3 in mind, and appropriately tagged, are able to express a much larger range of colors, with deeper and more saturated tones. This effect may be subtle, but allows for the creation of more vibrant and authentic-looking assets.

# New in USD

- Updated and more efficient USD version
- Increased renderer feature support
- Updated documentation

All apple's first party applications, such as Motion and Quick Look, now benefit from an updated and more efficient USD version. USD supports a wide range of object types, also known as schemas.

This update also allows the Storm renderer in Preview on macOS to support rendering even more USD schemas and features.

## New RealityKit USD schemas

- Component
- Custom component
- Structs and dictionaries
- Audio File, Audio File Group, and Mix Group

USD also allows for custom schema types. And this year, RealityKit is introducing new Component schemas for its Entity Component System, or ECS for short, on xrOS.

RealityKit's ECS splits the systems that process data from the Component data itself, allowing it to live alongside 3D content. Thanks to these custom schemas, we can now use RealityKitComponent for built-in Components, and RealityKitCustomComponent for our own Swift custom components.

The Swift components structs and dictionaries can be represented by the equivalent RealityKit USD schemas. RealityKit also builds upon USD's spatialAudio with RealityKit's Audio File, Audio File Group, and MixGroup to create even more immersive audio.

Let's take a look at a USD file that represents some custom component data, as a USD prim, which is what USD calls objects in its hierarchy.

```swift
// Character.usda
def RealityKitCustomComponent "MyProject_PointsComponent" {
	int points = 75
	uniform token info:id = "MyProject.PointsComponent"
}
```

This allows custom component data to live alongside other prims such as geometry. Since this is all in USD, we can use any app that lets you author USD prims directly to create them alongside the rest of your scene.

```swift
// PointsComponent.swift
public struct PointsComponent: Component, Codable {
	var points: Int = 100
	
	public init() { }
```

This aligns with the corresponding Swift Component that can then be used to read these values from other USD components, such as here where different objects in the app may have specific Engagement Points associated with them.

Please check out the talks on building applications with Reality Composer Pro to learn more.

[Work with Reality Composer Pro content in Xcode](https://developer.apple.com/videos/play/wwdc2023/10273/)

## Industry support
- Growing ecosystem  
- Easy to build for iOS  
- Reduced dependencies  
- Metal support in Hydra Storm  

Apple worked with Pixar and the community to list many of the software packages that now support USD on the OpenUSD webpage. This allows creators to see how easily they can create USD-based content with their own existing workflows on a Mac. And it also been working to build USD for portable platforms like iOS, so that developers, can integrate USD into your their applications that can author immersive USD content.

USD includes a technology called Hydra, an abstraction framework for renderers, and Storm, a real-time renderer that makes use of Hydra. Apple has worked with Pixar to add Metal support to Storm, making use of modern graphics API that enables developers to create high-performance, GPU-based applications on Apple platforms.

The Animal Logic ALab scene is representative of many feature film-level assets. When set to full resolution, this scene can take over 26GB of graphics memory, previously requiring desktop workstation GPUs.

![USD and MaterialX][content10]

[content10]: WWDC23-10086-content10

Now, with Metal in Hydra Storm, and unified memory on Apple silicon, a MacBook Pro is enough to work on the go, even on demanding scenes like this, while retaining interactive performance. This high-performance rendering in Storm also enables Blackmagic Design to add fast viewport rendering of USD to Fusion in DaVinci Resolve.

![USD and MaterialX][content11]

[content11]: WWDC23-10086-content11

Building on the collaboration from previous years, Apple is working with Autodesk on their open source Maya USD plugin.

## Maya USD plug-in
- Enhanced asset export
- Better animation import
- Easier rOS workflows

Apple has made several contributions to the project, including enhancements to the export of geometry and materials. There are also improvements to animation import. All of this helps to have more seamless workflows to create spatial content for xrOS. (Some of these features may be released in later releases of Maya USD)

## Blender
- Better USD import and export
- USDZ support
- Metal rendering

Apple has been working with the Blender Foundation, many individuals and partners like AMD, NVIDIA, and Unity, to deliver updates to Blender, an open-source 3D application. This collaboration has enabled significantly improved USD import and export in Blender 3.5.

This includes USDZ support for the first time. Apple also worked with the Blender Foundation to introduce Metal support for their Eevee and Cycles renderer. Now with Blender 3.5, we can run Blender as a fully native Metal application, speeding up our UI, viewport, and final render. Final renders can make use of the GPU to complete in up to half the time when compared to CPU based renders, and the viewport can now render up to 4 times faster than OpenGL in certain scenes.

![USD and MaterialX][content12]

[content12]: WWDC23-10086-content12


## Resources
[Have a question? Ask with tag wwdc2023-10086](https://developer.apple.com/forums/create/question?tag1=795030&tag2=724030&tag3=251)  
[Search the forums for tag wwdc2023-10086](https://developer.apple.com/forums/tags/wwdc2023-10086)  
[Validating feature support for USD files](https://developer.apple.com/documentation/RealityKit/validating-usd-files)

## Related Videos
[Build spatial experiences with RealityKit - WWDC23](https://developer.apple.com/videos/play/wwdc2023/10149)  
[Create 3D models for Quick Look spatial experiences - WWDC23](https://developer.apple.com/videos/play/wwdc2023/10167)  
[Explore materials in Reality Composer Pro - WWDC23](https://developer.apple.com/videos/play/wwdc2023/10164)  
[Meet Reality Composer Pro - WWDC23](https://developer.apple.com/videos/play/wwdc2023/10165)  
[Work with Reality Composer Pro content in Xcode](https://developer.apple.com/videos/play/wwdc2023/10273/)
