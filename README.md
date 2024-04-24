# QR code generator using Python
This script take a link of any URL and generate a `QR code` corresponding to it.
### Prerequisites
`Python 3`
### Library Used
* [qrcode](https://github.com/lincolnloop/python-qrcode)

### To install required external modules
Run `pip install qrcode` 

### How to run the script
- Provide your desired URL in the script
- Execute `python3 QR_code_generator.py`

### Screenshot showing the sample use of the script
<p align="center">
  <a href="output 1.png"><img src="https://user-images.githubusercontent.com/85709371/151921721-132e76c1-1604-49ad-9234-1ef3cc9ac45b.png" alt="url_qrcode"></a>
</p>

##Program
```
import qrcode
import logging
import traceback
from logging.handlers import RotatingFileHandler

logging.basicConfig(handlers=[RotatingFileHandler('qr_generation.log', maxBytes=10000, backupCount=3, encoding='utf-8')],
                    level=logging.INFO,
                    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s')

def generate_qr_code(product, weight, mrp, packing_date):
    details = f"Product: {product}\nWeight: {weight}\nMRP: Rs.{mrp}\nPacking Date: {packing_date}"

    logging.info('Starting QR code generation process.')
    logging.debug(f'QR code details: {details}')

    try:
        qr = qrcode.QRCode(
            version=1,
            error_correction=qrcode.constants.ERROR_CORRECT_L,
            box_size=15,
            border=4,
        )
        logging.debug('QR code instance created.')

        qr.add_data(details)
        logging.debug('Data added to QR code.')

        qr.make(fit=True)
        logging.debug('QR code fitting is done.')

        # convert into image
        img = qr.make_image(fill_color="green", back_color="white")
        img.save("myqr.png")
        logging.info('QR code image saved successfully.')
        print("QR code details:\n", details) 
    except Exception as e:
        logging.error(f'Error during QR code generation: {e}')
        logging.error(traceback.format_exc()) 
if __name__ == "__main__":
    product = "Toor Dal"
    weight = "1 kg"
    mrp = 100
    packing_date = "15-01-2024"
    generate_qr_code(product, weight, mrp, packing_date)

```


## *Author Name*
[Vikrant](https://github.com/vikrant-v28)
