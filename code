import hashlib
import sys
import bcrypt
import time
import os

def mode():
	global mode
	mode = input("\nPlease select a mode:\n1. Loop Encode\n2. Mass Encode\n")
	while not mode in ['1', '2']:
		mode = input("Please select a mode:\n1. Loop Encode\n2. Mass Encode\n")
	mode = int(mode)

def encoding(string, lang):
	global timetaken
	bt = time.perf_counter()
	utf = string.encode(encoding = 'utf-8')
	langencode = eval(f"hashlib.{lang}(utf)")
	lis = str(langencode).split()
	lis = lis[4].split('>')
	bytes = langencode.digest()
	at = time.perf_counter()
	timetaken = str(round(at-bt, 6))
	print(f"\nOne string encoded.\nOriginal String: {string}\nEncoded String: {bytes}\nSize: {sys.getsizeof(bytes)}\nMemory Address: {lis[0]}\nTime Taken: {timetaken} seconds\n")
	time.sleep(1)
	
def bcryptencode(string):
	global timetake
	bt = time.perf_counter()
	print("\nGenerating salt...")
	salt = bcrypt.gensalt(14)
	print("Salt generated.\nEncrypting...")
	hash = bcrypt.hashpw(string, salt)
	at = time.perf_counter()
	timetake = str(round(at-bt, 2))
	print(f"\nOne string encoded.\nOriginal String: {string}\nEncrypted String: {hash}\nTime Taken: {timetake} seconds")
	return ""
	
def langask():
	global lang
	lang = input("\nEnter the encoding language you want to use:\n1. Sha256\n2. Md5 hash\n3. Bcrypt (might take awhile)\n4. pbkdf2 (most secure)\n")
	while lang not in ['1', '2', '3', '4']:
		lang = input("Enter the encoding language you want to use:\n1. Sha256\n2. Md5 hash\n3. Bcrypt (might take awhile)\n4. pbkdf2 (most secure)\n")
	
	if lang == '1':
		lang = 'sha256'
	elif lang == '2':
		lang = 'md5'
		
def pbkdf2(string):
	global timetake
	bt = round(time.perf_counter(), 5)
	print('\nGenerating salt...')
	salt = os.urandom(300)
	key = hashlib.pbkdf2_hmac('sha256', string.encode('utf-8'), salt, 550000)
	timetake = round(time.perf_counter(), 5) - bt
	print(f"One string encoded.\nOriginal String: {string}\nEncoded String: {key}\nTime Taken: {timetake} seconds")
	return ""
	
	
def massCode():
	strings = []
	global timetake
	while True:
		string = input("\nEnter your text for mass encode. ('-' to stop)\n")
		if string == '-':
			break
		strings.append(string)
		
	if lang == '3':
		
		bt = time.perf_counter()
		[print(i) for i in map(bcryptencode, strings)]
		at = time.perf_counter()
		timetake = str(round(at-bt, 6))
		print(f"Total time taken for operation: {timetake} seconds")
		
	elif lang == '4':
		bt = time.perf_counter()
		[print(i) for i in map(pbkdf2, strings)]
		at = time.perf_counter()
		timetake = str(round(at-bt, 6))
		print(f"Total time taken for operation : {timetake} seconds")
		
	else:
		[encoding(i, lang) for i in strings]
	
def loopCode():				
	while True:
		string = input("\nEnter your text to be encoded here.(Enter '-1' to stop, -2 to change encoding language)\n")
		if string == '-1':
			break
		elif string == '-2':
			langask()
			string = input("\nEnter your text to be encoded here (Enter '-1' to stop, '-2' to change encoding language)\n")
		if lang == '3':
			bcryptencode(string)
			
		elif lang == '4':
			pbkdf2(string)
			
		else:
			encoding(string, lang)

						
langask()		
mode()
if mode%2:
		loopCode()
else:
		massCode()
