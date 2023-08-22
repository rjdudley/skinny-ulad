# Background

When Fannie Mae and Freddie Mac redesigned their application forms into the Uniform Residential Loan Application (aka "URLA" or "1003"), they also adopted an industry standard named MISMO as the data schema for the Uniform Loan Application Dataset (ULAD), which is the XML format used to transmit the application data collected on the URLA or a similar mechanism.  There is a big initiative by federal agencies to adopt industry standards to ease the development burden.  MISMO has been around a long time and there is a lot of industry experience with it.  For reference, and mapping the URLA fields to ULAD data elements, see the ULAD Mapping Document link at the bottom of https://singlefamily.fanniemae.com/delivering/uniform-mortgage-data-program/uniform-residential-loan-application.  There are other MISMO-based datasets used by Fan and Fred, such as the UCD and ULDD, but this project focuses on the ULAD only.

As a data architect. I was responsible for develping schemas for internal use.  As with Fan and Fred, we saw the value of adopting and adapting industry standards internally, and MISMO was one we wanted to use.  This design came from my frustration with the XML format and is also a sign I should focus on my other hobbies because who in their right mind does this in their spare time?

# Why is MISMO/ULAD Unsuitable for APIs?

MISMO is an extensive specifiication, meant to cover all the data needs in all the uses of the mortgage industry in one document.  You need a lot of RAM just to open the full schema in an XML modeling tool.  It was initially designed for large transfers of mortgage info, on the scale of 100s-1000s of documents, in a highly normalized using arcroles.  It's like EDI via XML.  And that's fine, very suitable for a certain use case.

Because it was meant to be normalized and contain a lit of documents, it's very deeply nested.  Following the XML specification you're something like 17 layers of XML markup before you hit your first piece of data (I no longer have access to MISMO and don't remember exactly, but it's around that).  Even when a use case specific subset is designed (like the ULAD or UCD), the XML honors this deep nesting.  And that's the problem.  Modern APIs are designed for accessing single resources, use JSON as the format, and have a flat or shallow nesting.

# What is the Skinny ULAD?

As we moved toward a services oriented architecture, heavy on REST-ful APIs, I wanted to keep the governance of the MISMO dictionary, but create a more API friendly format.  There are two editions--one with a shallow nesting of hierarchical or repeated data, and another which is completely flattened.

This isn't what I'd consider final, but I'm probably not putting additional effort into this unless I end up in the mortgage industry again.

# What are the x- elements?

Those are not part of MISMO, but are common internal data elements.  I took inspiration from the "x-" properties of HTML headers for the naming convention.

# What's included?

At the top level are the two schema definition files.  Folders contain forward-engineered JSON schemas of the respective definitions.  I'd do an OpenAPI version but that requires a more expensive version of the tool than I can personally afford.

# What Modeling Tool Was Used?

This model was developed with Hackolade, which I think is the best modeling tool on the market.  Check it out at [https://hackolade.com/](https://hackolade.com/).  The Personal edition I use is very feature-rich and good for a lot of things.
