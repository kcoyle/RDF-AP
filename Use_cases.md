# Use Cases

## Multiple sources

I have more than one source of input, and they have some differences between them. I want to be able to gather this information in a single profile so I can mix that data with my own. Here is an example:

Source A has an "address" field that puts the entire address into a single string, like:

  3333 Main Street, Arlington, Virginia, 10010

Source B has an "address" structure that uses Vcard:

  ADR;HOME:;;42 Plantation St.;Baytown;LA;30314;USA

Source C uses the following structure:
<pre>
  AddressId
  Line1
  Line2
  Line3
  City
  ZipOrPostcode
  StateProvinceCounty
  CountryId
  OtherAddressDetails</pre>