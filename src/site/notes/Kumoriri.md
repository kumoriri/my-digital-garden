```dataview
>> TABLE WITHOUT ID
>>   file.link AS "文件名",
>>   dateformat(file.mtime, "MM-dd") AS "修改日期"
>> FROM ""
>> WHERE file.name != this.file.name
>> SORT file.mtime DESC
>> LIMIT 10
>> ```