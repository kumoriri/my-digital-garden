```dataview
>> LIST
>> FROM ""
>> WHERE file.name != this.file.name
>> SORT file.mtime DESC
>> LIMIT 10
>> ```