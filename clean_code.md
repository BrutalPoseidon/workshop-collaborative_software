![The only valid measurement of code quality: WTFs/minute](resources/measuring_code_quality.jpg)

--

# Clean Code

* ... is not about formatting style

> Code I'm not afraid to modify

[g andrieu, Stack Overflow](https://stackoverflow.com/questions/954570/definition-of-clean-code)

--

# Clean Code (2)

* Easy to understand
* Easy to modify
* Easy to test
* Does not contain duplicated code
* Works correctly

--

## Code Rotting

* Code gets worse over time
* Code gets worse with number of developers <!-- .element: class="fragment" -->

Instead, every time you look at a piece of code, improve it a bit <!-- .element: class="fragment" -->

* Refactoring of names of variables or methods <!-- .element: class="fragment" -->
* Shortening of methods that are too complex/long <!-- .element: class="fragment" -->
* Deduplicate code <!-- .element: class="fragment" -->
* ... <!-- .element: class="fragment" -->

--

> `assert` No Indico Developer attending the workshop?

--

## What is wrong here?

    def daysInYear(year):
        days = 365
        if (year % 4 == 0 and year % 100 != 0) or year % 400 == 0:
            days += 1
        return days

--

## What is wrong here? (2)

	def _initStandardPersonalData(self):
	    self._data = PersistentMapping()
	    self._sortedKeys = PersistentList()
	    p = PersonalDataFormItem({'id':'title', 'name': "Title", 'input':'list', 'mandatory':False})
	    self._data[p.getId()] = p
	    self._sortedKeys.append(p.getId())
	    p = PersonalDataFormItem({'id':'firstName', 'name': "First Name", 'input':'text', 'mandatory':True})
	    self._data[p.getId()] = p
	    self._sortedKeys.append(p.getId())
	    p = PersonalDataFormItem({'id':'surname', 'name': "Surname", 'input':'text', 'mandatory':True})
	    self._data[p.getId()] = p
	    self._sortedKeys.append(p.getId())
	    p = PersonalDataFormItem({'id':'position', 'name': "Position", 'input':'text', 'mandatory':False})
	    self._data[p.getId()] = p
	    self._sortedKeys.append(p.getId())
	    p = PersonalDataFormItem({'id':'institution', 'name': "Institution", 'input':'text', 'mandatory':True})
	    self._data[p.getId()] = p
	    self._sortedKeys.append(p.getId())
	    p = PersonalDataFormItem({'id':'address', 'name': "Address", 'input':'text', 'mandatory':False})
	    self._data[p.getId()] = p
	    self._sortedKeys.append(p.getId())
	    p = PersonalDataFormItem({'id':'city', 'name': "City", 'input':'text', 'mandatory':True})
	    self._data[p.getId()] = p
	    self._sortedKeys.append(p.getId())
	    p = PersonalDataFormItem({'id':'country', 'name': "Country/Region", 'input':'list', 'mandatory':True})
	    self._data[p.getId()] = p
	    self._sortedKeys.append(p.getId())
	    p = PersonalDataFormItem({'id':'phone', 'name': "Phone", 'input':'text', 'mandatory':False})
	    self._data[p.getId()] = p
	    self._sortedKeys.append(p.getId())
	    p = PersonalDataFormItem({'id':'fax', 'name': "Fax", 'input':'text', 'mandatory':False})
	    self._data[p.getId()] = p
	    self._sortedKeys.append(p.getId())
	    p = PersonalDataFormItem({'id':'email', 'name': "Email", 'input':'hidden', 'mandatory':True})
	    self._data[p.getId()] = p
	    self._sortedKeys.append(p.getId())
	    p = PersonalDataFormItem({'id':'personalHomepage', 'name': "Personal homepage", 'input':'text', 'mandatory':False})
	    self._data[p.getId()] = p
	    self._sortedKeys.append(p.getId())

--

## What is wrong here? (3)

	def setConference( self, params ):
        if not ("confId" in params.keys()) and "confid" in params.keys():
            params["confId"] = params["confid"]
        if not ("confId" in params.keys()) and "conference" in params.keys():
            params["confId"] = params["conference"]
        if isinstance(params.get("confId", ""), list):
            params["confId"] = params["confId"][0]
        if not ("confId" in params.keys()) or \
           params["confId"] == None or \
               params["confId"].strip()=="":
            raise errors.MaKaCError( _("conference id not set"))
        self.__confId = params["confId"]
