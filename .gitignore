import os
import getopt
import sys

try:
    from PIL import Image, ImageDraw, ImageFont, ImageEnhance
except:
    print "To use this program, you need to install Python Imaging Library - http://www.pythonware.com/products/pil/"
    sys.exit(1)
	
def watermark(im, wm_text):

    if im.mode != 'RGBA':
        im = im.convert('RGBA')
        
    else:
        print "RBGA true"
        
    im = im.transpose(Image.ROTATE_270)

    textdraw = ImageDraw.Draw(im)

    fontsFolder = 'C:\Windows\Fonts' # e.g. 'Library/Fonts'
    arialFont = ImageFont.truetype(os.path.join(fontsFolder, 'arial.ttf'), 12)

    textdraw.text((4,im.size[1]-14), wm_text, fill=(180,180,180,255), font = arialFont)

    return im
	
# Let's parse the arguments.
opts, args = getopt.getopt(sys.argv[1:], 'w:')

pathname = os.path.dirname(sys.argv[0])

# Set some default values to the needed variables.
directoryIN = os.path.abspath(pathname) + '\\In'
directoryOUT = os.path.abspath(pathname) + '\\Out'

width = -1

# If an argument was passed in, assign it to the correct variable.
for opt, arg in opts:
    if opt == '-w':
        width = int(arg)

# We have to make sure that all of the arguments were passed.
if width == -1:
    print('Invalid command line arguments.' \
          '-w [width] are required')
 
    # If an argument is missing exit the application.
    exit()

for image in os.listdir(directoryIN):
    print('Resizing image ' + image)
 
    # Open the image file.
    img = Image.open(os.path.join(directoryIN, image))

    [x,y] = img.size
    
    if x > y: # Landscape mode
        #print('Horizontal')    
        
        # Calculate the height
        widthPercent = (width / float(img.size[0]))
        height = int((float(img.size[1]) * float(widthPercent)))

        # Resize it
        img = img.resize((width, height), Image.ANTIALIAS)		
		
    else: # Portrait mode
        #print('Vertical')
        
        # Calculate the height        
        vert_width = width - 250

		# Exit if width is too small

        if vert_width > 0:
            pass
        else:
            print("Common bro, '-w' parameter should be more than 250(!)")
            sys.exit(1)
        
        # Calculate the height
        widthPercent = (vert_width / float(img.size[0]))
        height = int((float(img.size[1]) * float(widthPercent)))
        
        # Resize it
        img = img.resize((vert_width, height), Image.BICUBIC)        
	

    img = watermark(img, u"\u00A9" + " Volodymyr Sieroshtan")	
    img = img.transpose(Image.ROTATE_90)

    # Save it back to disk
    img.save(os.path.join(directoryOUT, 'E' + image[4:]), quality=70, optimize=True, progressive=True)
 
print('Batch processing complete.')
