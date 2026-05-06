# 🚀 เริ่มต้นเรียนรู้ Angular (Angular Beginner Guide)
ยินดีต้อนรับสู่โปรเจกต์สำหรับฝึกฝนและเรียนรู้ Angular Framework เบื้องต้น! โปรเจกต์นี้รวบรวมพื้นฐานที่จำเป็น ตั้งแต่การติดตั้งไปจนถึงการจัดการข้อมูลในระดับเบื้องต้น

## 🛠️ สิ่งที่ต้องเตรียม (Prerequisites)
ก่อนเริ่มต้น ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้งสิ่งเหล่านี้เรียบร้อยแล้ว:
* [Node.js](https://nodejs.org/en/download): (เวอร์ชันล่าสุดหรือ LTS)
* npm (ติดตั้งมาพร้อมกับ Node.js)
* [Angular CLI](https://angular.dev/overview): ติดตั้งผ่านคำสั่ง:

``` npm install -g @angular/cli ```

## 🏗️ โครงสร้างโปรเจกต์ (Project Structure)
ใน Angular เวอร์ชันใหม่ (Stand-alone components) โครงสร้างหลักจะอยู่ที่โฟลเดอร์ src/app:

**Components:** ส่วนประกอบของหน้าจอ (UI)
**Services:** ส่วนที่ใช้จัดการ Logic หรือดึงข้อมูลจาก API
**Models/Interfaces:** กำหนดโครงสร้างข้อมูล (TypeScript)
**Styles:** การตกแต่งด้วย [Tailwind CSS](https://tailwindcss.com/docs/installation/using-vite) หรือ CSS ปกติ


## 📘 หัวข้อการเรียนรู้ (Learning Path)
**1. Component & Template**
เรียนรู้การสร้าง Component และการใช้ Control Flow แบบใหม่ (@if, @for)

```
@for (item of items; track item.id) {
  <div class="p-4 border-b">
    {{ item.name }}
  </div>
}
```
**2. Data Binding**
* Interpolation: `{{ value }}` แสดงค่าจาก TypeScript สู่ HTML
* Property Binding: `[property]="value"` ส่งค่าเข้า Property
* Event Binding: `(click)="method()"` จัดการเหตุการณ์ต่างๆ
* Two-way Binding: `[(ngModel)]="value"` (ต้อง Import FormsModule)

**3. Reactive Forms & Validations**
การจัดการฟอร์มที่มีความซับซ้อนและการตรวจสอบความถูกต้องของข้อมูล (Validation) โดยใช้ `FormGroup` และ `FormArray`

**4. Directives & Pipes**
* Directives: การควบคุม DOM เช่น `[ngClass], [ngStyle]` หรือการใช้ CDK (Component Dev Kit) สำหรับฟีเจอร์เช่น Drag & Drop
* Pipes: การแปลงรูปแบบข้อมูลใน Template เช่น `| date, | json, | async`


## 🧪 คำสั่งที่ใช้บ่อย (Useful CLI Commands)
* สร้าง Component ใหม่: ```ng generate component components/name```
* สร้าง Service ใหม่: ```ng generate service services/name```
* Build สำหรับ Production: ```ng build```


## 📂 โครงสร้างโฟลเดอร์ (Project Structure)
```
src/
├── app/
│   ├── components/      # ส่วนประกอบหน้าจอ (Header, Table, Form)
│   ├── models/          # Interfaces และ Types (TypeScript)
│   ├── services/        # Logic สำหรับจัดการข้อมูลและ API
│   └── app.component.ts # จุดเริ่มต้นหลักของแอป
├── assets/              # ไฟล์รูปภาพหรือ Static files
└── styles.css           # Global styles (Tailwind directives)
```


## 📂 การส่ง data ข้าม component
*1. Parent ➝ Child
```
// child.component.ts
@Input() data: string;
```

```
<!-- parent.component.html -->
<app-child [data]="parentData"></app-child>
```

*2. Child ➝ Parent

``` 
// child.component.ts
@Output() sendData = new EventEmitter<string>();

send() {
  this.sendData.emit('hello');
}
```

```
<!-- parent.component.html -->
<app-child (sendData)="handleData($event)"></app-child>
```

*3. Component ที่ไม่เกี่ยวกัน (Sibling / Cross component)
```
// data.service.ts
private dataSource = new BehaviorSubject<string>('default');
currentData$ = this.dataSource.asObservable();

setData(value: string) {
  this.dataSource.next(value);
}
```

```
// component A (ส่ง)
this.dataService.setData('hello');
```

```
// component B (รับ)
this.dataService.currentData$.subscribe(data => {
  console.log(data);
});
```

*4. Routing (ส่งผ่าน URL)

```this.router.navigate(['/page'], { queryParams: { id: 1 } });```
```
this.route.queryParams.subscribe(params => {
  console.log(params['id']);
});
```

