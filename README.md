# SmarkDown

A pure Swift [markdown](http://daringfireball.net/projects/markdown/) implementation consistent with Gruber's 1.0.1  version. It is released under the BSD license so please feel free to use (at your own risk). 

Pull requests are ***very*** welcome, see the vision for where I would like this to go. 

## Vision

Version 1.0 is a very minor Swift-ification of Gruber's original Perl implementation. Lots of regular expressions. The initial performance of this implementation yielded about 28s to process the large Markdown Syntax test. This has improved in 1.0.2 to 7s with some pretty simple optimization of what's there. 

However, I would next like to achieve two things

 1. Refactor to support easier extension for particular variants of Markdown
 2. Change the fundamental strategy from regular expressions to a higher performance scanner. In fact there are some seeds already sown there, but I want to clear out regular expressions. They are slow, opaque and the implementation has significant overhead. 

Once again, I would ***love*** to receive pull requests towards this goal. 

## Use
There are two ways to use it, it provides an extension to String so you can simply do

    let myString = "# Cool\n\nThis markdown'd\n"
    print(myString.markdown)

or you can explicitly create an instance (which will have some minor performance improvements for repeated calls

    let smarkDown = SmarkDown()
    print(smarkDown.markdown(myString))

## Integrating with your project
SmarkDown uses the [Swift Package Manager](https://swift.org/package-manager/) so if you are using this for your builds you simply need to add a dependency to your manifest

	import PackageDescription
	
	let package = Package(
		name : "Your Project",
		dependencies : [
			//Add the SmarkDown dependency
			.Package(url:"https://github.com/SwiftStudies/SmarkDown.git", majorVersion:1),
		]
	)

Alternatively you can clone (or download) the repository to your computer and add the following files (if you are cloning then I would suggest adding without copying) to your project

 * `SmarkDown.swift`
 * `SpecialCharacters.swift`
 * `Strings.swift`
 * `RegularExpressions.swift`
 
I'd recommend doing this in another target (such as library or framework) as there are some extensions you may not want to be exposed to (i.e. are internal to the module). 

## Reporting Issues

Please do so using Github's own system. 
