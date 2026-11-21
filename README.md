boy_bgr = cv2.imread("boy.jpg", cv2.IMREAD_COLOR)
assert boy_bgr is not None
boy_rgb = cv2.cvtColor(boy_bgr, cv2.COLOR_BGR2RGB)
print("Boy image shape:", boy_rgb.shape)
plt.figure(figsize=(8, 5))
plt.imshow(boy_rgb)
plt.axis("off")
plt.show()```

#### 15. Adjust the brightness of the image.
```python
brightness_matrix = np.full(boy_rgb.shape, 50, dtype=np.uint8)
print("Brightness change:", brightness_matrix[0, 0])
```

#### 16. Create brighter and darker images.
```python
boy_brighter = cv2.add(boy_rgb, brightness_matrix)
boy_darker = cv2.subtract(boy_rgb, brightness_matrix)
```

#### 17. Display the images (Original Image, Darker Image, Brighter Image).
```python
fig, ax = plt.subplots(1, 3, figsize=(14, 4))
for a, im, title in zip(ax, [boy_rgb, boy_darker, boy_brighter], ["Original", "Darker (−50)", "Brighter (+50)"]):
    a.imshow(im); a.set_title(title); a.axis("off")
plt.tight_layout(); plt.show()
```

#### 18. Modify the image contrast.
```python
# Alpha > 1 increases contrast; alpha < 1 reduces contrast.
# Beta shifts brightness so the scaling is around mid-gray (128).
def adjust_contrast(image, alpha):
    return np.clip((image.astype(np.float32) - 128) * alpha + 128, 0, 255).astype(np.uint8)

boy_lower_contrast = adjust_contrast(boy_rgb, 0.8)
boy_higher_contrast = adjust_contrast(boy_rgb, 1.2)
# Additional 1.1× result, as mentioned in the supplied exercise:
boy_contrast_1_1 = adjust_contrast(boy_rgb, 1.1)
```

#### 19. Display the images (Original, Lower Contrast, Higher Contrast).
```python
fig, ax = plt.subplots(1, 3, figsize=(14, 4))
for a, im, title in zip(ax, [boy_rgb, boy_lower_contrast, boy_higher_contrast], ["Original", "Lower contrast (0.8×)", "Higher contrast (1.2×)"]):
    a.imshow(im); a.set_title(title); a.axis("off")
plt.tight_layout(); plt.show()
```

#### 20. Split the image (boy.jpg) into the B,G,R components & Display the channels.
```python
b, g, r = cv2.split(boy_bgr)
fig, ax = plt.subplots(1, 3, figsize=(13, 4))
for a, channel, title in zip(ax, [b, g, r], ["Blue", "Green", "Red"]):
    a.imshow(channel, cmap="gray", vmin=0, vmax=255); a.set_title(title); a.axis("off")
plt.tight_layout(); plt.show()
```

#### 21. Merged the R, G, B , displays along with the original image
```python
merged_rgb = cv2.merge([r, g, b])
fig, ax = plt.subplots(1, 2, figsize=(11, 4))
for a, im, title in zip(ax, [boy_rgb, merged_rgb], ["Original RGB", "Merged RGB"]):
    a.imshow(im); a.set_title(title); a.axis("off")
plt.tight_layout(); plt.show()
print("Identical:", np.array_equal(boy_rgb, merged_rgb))
```

#### 22. Split the image into the H, S, V components & Display the channels.
```python
hsv_img = cv2.cvtColor(boy_bgr, cv2.COLOR_BGR2HSV)
hue, saturation, value = cv2.split(hsv_img)
fig, ax = plt.subplots(1, 3, figsize=(13, 4))
for a, ch, title in zip(ax, [hue, saturation, value], ["Hue (0–179)", "Saturation (0–255)", "Value (0–255)"]):
    a.imshow(ch, cmap="gray"); a.set_title(title); a.axis("off")
plt.tight_layout(); plt.show()
```
#### 23. Merged the H, S, V, displays along with original image.
```python
merged_hsv = cv2.merge([hue, saturation, value])
restored_bgr = cv2.cvtColor(merged_hsv, cv2.COLOR_HSV2BGR)
restored_rgb = cv2.cvtColor(restored_bgr, cv2.COLOR_BGR2RGB)
fig, ax = plt.subplots(1, 2, figsize=(11, 4))
for a, im, title in zip(ax, [boy_rgb, restored_rgb], ["Original RGB", "Restored from HSV"]):
    a.imshow(im); a.set_title(title); a.axis("off")
plt.tight_layout(); plt.show()
print("Max rounding difference:", np.abs(boy_rgb.astype(int) - restored_rgb.astype(int)).max())
```

## Output:
- **i)** Read and Display an Image.  
- **ii)** Adjust Image Brightness.  
- **iii)** Modify Image Contrast.  
- **iv)** Generate Third Image Using Bitwise Operations.
<img width="660" height="218" alt="image" src="https://github.com/user-attachments/assets/415bcb43-48b7-4d52-8e2c-e635ba0b08d5" />
<img width="703" height="257" alt="image" src="https://github.com/user-attachments/assets/5e9165d0-b46f-4ba9-89c4-60cf6fdf71b1" />
<img width="680" height="644" alt="image" src="https://github.com/user-attachments/assets/8780982b-6af9-4a0c-b4bb-cc032f7a09b3" />

<img width="783" height="202" alt="image" src="https://github.com/user-attachments/assets/f714079e-d7ba-4650-b5f9-c409e84f03cc" />
<img width="756" height="272" alt="image" src="https://github.com/user-attachments/assets/356169f7-148f-4035-aadf-5e87eafc2ca1" />
<img width="828" height="647" alt="image" src="https://github.com/user-attachments/assets/5b4b8e94-37ba-4fdb-abeb-d47f9d937513" />
<img width="816" height="663" alt="image" src="https://github.com/user-attachments/assets/a577eac1-b389-4eb6-9316-a6c5ee1da9af" />
<img width="830" height="688" alt="image" src="https://github.com/user-attachments/assets/6a15ea19-d1ec-4546-8d93-fc16b0dbd0b6" />
<img width="800" height="642" alt="image" src="https://github.com/user-attachments/assets/8c426c69-b1be-41bc-93c1-a54744cdd5b8" />
<img width="827" height="666" alt="image" src="https://github.com/user-attachments/assets/78b69e4c-372e-4747-a2dd-7f02add5215e" />
<img width="843" height="658" alt="image" src="https://github.com/user-attachments/assets/b1580fd5-6f9e-4366-b6b9-288757887054" />
<img width="733" height="675" alt="image" src="https://github.com/user-attachments/assets/4591ec4d-2ae7-4c0b-9c32-7d48fa711e64" />
<img width="1246" height="678" alt="image" src="https://github.com/user-attachments/assets/34d8ef07-7b22-447a-bf2a-041d47d907c2" />
<img width="724" height="493" alt="image" src="https://github.com/user-attachments/assets/22b4a832-b8ca-41fe-b9dc-29c5bfcd2bd6" />
<img width="723" height="267" alt="image" src="https://github.com/user-attachments/assets/0df8258c-1f91-4973-9212-85b99e401ae3" />
<img width="693" height="384" alt="image" src="https://github.com/user-attachments/assets/fa9989f8-8560-421e-9923-8797e66e595b" />
<img width="713" height="398" alt="image" src="https://github.com/user-attachments/assets/f59c2ef6-d483-42f0-ad39-bf156889e767" />
<img width="706" height="497" alt="image" src="https://github.com/user-attachments/assets/1416e196-d4ec-4fc6-88d3-97e72b1ff246" />
<img width="718" height="433" alt="image" src="https://github.com/user-attachments/assets/e1bb2283-6551-4227-92f0-65c07aab3f51" />
<img width="713" height="558" alt="image" src="https://github.com/user-attachments/assets/a00d433a-36b3-4160-893e-460354c14fe6" />

## Result:
Thus, the images were read, displayed, brightness and contrast adjustments were made, and bitwise operations were performed successfully using the Python program.
