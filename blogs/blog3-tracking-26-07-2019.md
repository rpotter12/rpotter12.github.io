# Tracking online WhatsApp status
(Publish date: 26 July 2019)<br><br>

WhatsApp Messenger is a freeware, cross-platform messaging and Voice over IP service owned by Facebook. It allows users to send text messages and voice messages, make voice and video calls, and share images, documents, user locations, and other media. 
<br><br>
Now a days people use WhatsApp more than other social media for sharing messages. They liked to talk and to share data to their family, friends and their loved ones on WhatsApp. Sometimes people wants to talk with their contacts but they are not online at that time. They get curious to know at what time they get online and for how much time they were online. They started keep open their contact's account and start tracking the online status. I'm one of them. I also have done these kind of stupid stuff. Some people use their WhatsApp messenger for a particular time period in a day. I hate late replies. I usually get late reply when I want to talk. The problem was she use WhatsApp for a period of time in a day. So to talk I need to know the time I started seeing online time.
<br><br>
I fed up with this. So being a programmer I created a software to track the online status. I used a very simple logic to create script for this purpose. I used Selenium library of python to open WhatsApp web. Then the user have to scan QR code. Then script find the target person by `x_arg = '//span[contains(@title, '+ '"' +target + '"'+ ')]'`. This is the path of the target. To navigate to that path I used selenium internal function. The code to find the path and to navigate to it is: 
```
x_arg = '//span[contains(@title, '+ '"' +target + '"'+ ')]'
person_title = wait.until(EC.presence_of_element_located((By.XPATH, x_arg)))
print(target)
person_title.click()
```
<br><br>
Then to get the online status I take the value of class `_315-i`. I used a logic that whenever the target get online/offline the time will be stored in status.txt file. To get the desire output I have used two infinte loops in this. The code for tracking online status is:
```
while True:
	i=0
	try:
		status = driver.find_element_by_class_name('_315-i').text
		i=1
	except (NoSuchElementException, StaleElementReferenceException):
		status = 'offline'
		i=0
	if i==1:
		playsound('plucky.mp3')
	print(datetime.datetime.now())
	print(status)
	f=open('status.txt','a')
	f.write(str(datetime.datetime.now()))
	f.write(status)
	f.close()
	while True:
		if i == 1:
			try:
				re_status = driver.find_element_by_class_name('_315-i').text
				continue
			except (NoSuchElementException, StaleElementReferenceException):
				re_status = 'offline'
				break
		else:
			try:
				re_status = driver.find_element_by_class_name('_315-i').text
				break
			except (NoSuchElementException, StaleElementReferenceException):
				re_status = 'offline'
				continue
	time.sleep(1)
```
<br><br>
The software I created to use this code is named whatsapp-play. The link of the software is [https://github.com/rpotter12/whatsapp-play](https://github.com/rpotter12/whatsapp-play). And the link of the online status tracking script is [https://github.com/rpotter12/whatsapp-play/blob/master/wplay/onlinetracker.py](https://github.com/rpotter12/whatsapp-play/blob/master/wplay/onlinetracker.py)