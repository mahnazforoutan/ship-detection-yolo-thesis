# ship-detection-yolo-thesis
کدهای پایان‌نامه کارشناسی ارشد - تشخیص کشتی با YOLO
# تشخیص کشتی با استفاده از الگوریتم‌های سری YOLO - پایان‌نامه کارشناسی ارشد

[![Python 3.12](https://img.shields.io/badge/python-3.12-blue.svg)](https://www.python.org/downloads/release/python-3129/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.10-red)](https://pytorch.org/)
[![Ultralytics](https://img.shields.io/badge/Ultralytics-8.4.12-green)](https://docs.ultralytics.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

این مخزن شامل کدها، مدل‌های آموزش‌دیده و نتایج پایان‌نامه کارشناسی ارشد با عنوان **«تشخیص کشتی از طریق پهپادها با استفاده از الگوریتم‌های سری YOLO»** است. در این پژوهش، چهار معماری YOLOv8m، YOLOv10m، YOLOv11m و YOLO26m برای تشخیص کشتی‌های دریایی روی دیتاست استاندارد SeaShips مقایسه شده‌اند.

## 📋 فهرست مطالب
- [معرفی پروژه](#معرفی-پروژه)
- [دیتاست](#دیتاست)
- [پیش‌نیازها و نصب](#پیش‌نیازها-و-نصب)
- [ساختار مخزن](#ساختار-مخزن)
- [آموزش مدل‌ها](#آموزش-مدل‌ها)
- [ارزیابی و نتایج](#ارزیابی-و-نتایج)
- [مدل‌های آموزش‌دیده](#مدل‌های-آموزش‌دیده)
- [چگونگی استفاده](#چگونگی-استفاده)
- [نتایج اصلی](#نتایج-اصلی)
- [نحوه استناد](#نحوه-استناد)
- [مجوز](#مجوز)

## 🎯 معرفی پروژه
هدف این پژوهش، مقایسه سیستماتیک چهار نسخه جدید YOLO (v8m، v10m، v11m و v26m) در تشخیص شش نوع کشتی از تصاویر پهپادی است. تمامی مدل‌ها با پارامترهای یکسان روی دیتاست SeaShips آموزش دیده و از نظر دقت (mAP@50، mAP@50-95)، سرعت استنتاج و مصرف منابع مقایسه شده‌اند.

**نوآوری‌های پژوهش:**
- اولین مقایسه جامع YOLOv10, v11, v26 در تشخیص کشتی
- تحلیل کمی تعامل دقت و سرعت (Trade-off) و شناسایی مرز بهینگی پارتو
- دستیابی به بالاترین دقت گزارش‌شده روی دیتاست SeaShips (99.37% mAP@50)

## 📊 دیتاست
از دیتاست استاندارد [SeaShips](https://github.com/... ) استفاده شده است که شامل 7000 تصویر با شش کلاس کشتی است:
- ore carrier
- fishing boat
- bulk cargo carrier
- general cargo ship
- container ship
- passenger ship

تقسیم‌بندی: 70% آموزش، 20% اعتبارسنجی، 10% تست.

##  پیش‌نیازها و نصب
پیش‌نیازهای نرم‌افزاری:
- Python 3.12
- PyTorch 2.10
- CUDA 12.8
- Ultralytics 8.4.12
- سایر کتابخانه‌ها: numpy, pandas, matplotlib, opencv-python, etc.

نصب کتابخانه‌های مورد نیاز:
```bash
pip install -r requirements.txt

 آموزش مدل‌ها به عنوان مثال، برای آموزش YOLOv8m:


from ultralytics import YOLO

model = YOLO('yolov8m.pt')
results = model.train(
    data='data/dataset.yaml',
    epochs=70,
    imgsz=640,
    batch=16,
    device=0,
    project='runs/train',
    name='yolov8m_seaships'
)

تمام پارامترهای آموزش برای همه مدل‌ها یکسان در نظر گرفته شده تا مقایسه منصفانه باشد.

 ارزیابی و نتایج
پس از آموزش، می‌توانید مدل‌ها را روی مجموعه تست ارزیابی کنید:


model = YOLO('models/yolov8m_best.pt')
metrics = model.val(data='data/dataset.yaml', split='test')
نتایج به صورت خودکار در پوشه results/ ذخیره می‌شوند.


مدل‌های آموزش‌دیده
فایل‌های وزن نهایی بهترین مدل‌ها در پوشه models/ قرار دارند

yolov8m_best.pt

yolov10m_best.pt

yolov11m_best.pt

yolo26m_best.pt

این مدل‌ها مستقیماً قابل استفاده برای تشخیص کشتی در تصاویر جدید هستند.

چگونگی استفاده
برای تشخیص روی یک تصویر جدید:


from ultralytics import YOLO

model = YOLO('models/yolov8m_best.pt')
results = model('path/to/image.jpg')
results.show()

 نتایج اصلی
جدول زیر خلاصه نتایج بهترین مدل‌ها را نشان می‌دهد:



مدل
        mAP@50	mAP@50-95	Precision	Recall	F1-Score	سرعت (ms/frame)
YOLOv8m	99.09%	83.67%	98.08%	96.87%	97.47%	3.2
YOLOv10m	97.89%	81.94%	94.99%	93.27%	94.12%	1.7
YOLOv11m	98.65%	82.48%	97.88%	96.63%	97.25%	3.1
YOLO26m	98.31%	83.12%	96.64%	95.84%	96.24%	3.1
مرز بهینگی پارتو: YOLOv10m (بهترین سرعت) و YOLOv8m (بهترین دقت)

### 📄 **فایل `requirements.txt`**


---

### 📄 **فایل `requirements.txt`**

```txt
torch>=2.10.0
ultralytics>=8.4.12
opencv-python>=4.11.0
numpy>=1.26.4
pandas>=2.2.2
matplotlib>=3.10.8
seaborn>=0.13.2
scikit-learn>=1.6.1
tqdm>=4.67.1
pillow>=10.4.0
pyyaml>=6.0.2

فایل data/dataset.yaml

# مسیر پایه (مطابق با سیستم خود تنظیم کنید)
path: /path/to/datasets/SeaShips_YOLO
train: images/train
val: images/val
test: images/test

# تعداد کلاس‌ها و نام‌ها
nc: 6
names:
  0: ore carrier
  1: fishing boat
  2: bulk cargo carrier
  3: general cargo ship
  4: container ship
  5: passenger ship

 تصاویر و نمودارها (پوشه results/figures/)
برای YOLOv8m (نتایج نهایی):

figures/confusion_matrices/yolov8m_confusion_matrix.png ← از فایل confusion_matrix (4).png (آخرین نسخه)

figures/curves/yolov8m_F1_curve.png ← از فایل BoxF1_curve (2).png (آخرین نسخه)

figures/curves/yolov8m_PR_curve.png ← از فایل BoxPR_curve (2).png (آخرین نسخه)

figures/curves/yolov8m_P_curve.png ← از فایل BoxP_curve (2).png

figures/curves/yolov8m_R_curve.png ← از فایل BoxR_curve (2).png

figures/validation_samples/yolov8m_val_batch0_labels.jpg ← از val_batch0_labels (4).jpg

figures/validation_samples/yolov8m_val_batch0_pred.jpg ← از val_batch0_pred (2).jpg

figures/validation_samples/yolov8m_val_batch1_labels.jpg ← از val_batch1_labels (2).jpg

figures/validation_samples/yolov8m_val_batch1_pred.jpg ← از val_batch1_pred (2).jpg

figures/validation_samples/yolov8m_val_batch2_labels.jpg ← از val_batch2_labels (3).jpg

figures/validation_samples/yolov8m_val_batch2_pred.jpg ← از val_batch2_pred (2).jpg

نمودار مقایسه نهایی:

figures/comparison_chart.png ← نمودار مقایسه‌ای مدل‌ها که از کد تولید می‌شود.

 جداول (پوشه results/tables/)
results_summary.csv: شامل نتایج کلی همه مدل‌ها (مطابق جدول ۴-۱ پایان‌نامه)

per_class_results.csv: شامل نتایج به تفکیک کلاس برای هر مدل

















