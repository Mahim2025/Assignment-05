1. What is the difference between getElementById, getElementsByClassName, and querySelector / querySelectorAll?

.getElementById(id)
একটি নির্দিষ্ট ID দিয়ে একটি HTML উপাদান নির্বাচন করে। শুধু একটি উপাদান ফেরত দেয়।
--const heartEl = document.getElementById('heartCount');

. getElementsByClassName(className)
একটি class এর সব উপাদান নির্বাচন করে। HTMLCollection দেয়।

.querySelector(selector)
CSS selector ব্যবহার করে প্রথম মিল পাওয়া উপাদান নির্বাচন করে।
--const firstCard = document.querySelector('.soft-card');

querySelectorAll(selector)
CSS selector ব্যবহার করে সব মিল পাওয়া উপাদান নির্বাচন করে। NodeList দেয়।
--const allCards = document.querySelectorAll('.soft-card');

-- ID একটির জন্য, Class সব মিলের জন্য, querySelector প্রথম মিলের জন্য, querySelectorAll সব মিলের জন্য।


2. How do you create and insert a new element into the DOM?

উত্তর:

ধাপ ১: নতুন উপাদান তৈরি করা
const li = document.createElement('li');

ধাপ ২: কনটেন্ট বা attribute সেট করা

li.textContent = "New History Item";
li.className = "history-item";

ধাপ ৩: DOM এ যুক্ত করা

const historyList = document.getElementById('historyList');
historyList.appendChild(li);

উপরের কোডে renderHistory() ফাংশনে এই ধাপগুলো ব্যবহার করা হয়েছে।


3. What is Event Bubbling and how does it work?
উত্তর:Event Bubbling হলো একটি ইভেন্টের parent element এর দিকে ধাপে ধাপে উঠে যাওয়া।উদাহরণ: যদি তুমি <button> এ ক্লিক করো, ইভেন্ট প্রথমে button, পরে parent div, তারপর body ইত্যাদিতে যায়।
<div id="parent">
  <button id="child">Click Me</button>
</div>
--document.getElementById('parent').addEventListener('click', () => alert('Parent clicked'));
--document.getElementById('child').addEventListener('click', () => alert('Child clicked'));
 Child ক্লিক করলে প্রথমে Child clicked পরে Parent clicked দেখাবে।


4. What is Event Delegation in JavaScript? Why is it useful?

উত্তর:
Event Delegation হলো parent element এ listener বসানো এবং child element এর ইভেন্ট হ্যান্ডেল করা।

ফায়দা:

নতুন child element এ আলাদা listener লাগবে না।

Memory ও performance কমে।
// একবার listener parent এ বসানো, child button handle করা
document.getElementById('cardGrid').addEventListener('click', e => {
  if (e.target.matches('[data-role="copyBtn"] i')) {
    alert('Copy button clicked');
  }
});

কোডে প্রতিটি কার্ডে আলাদা listener ব্যবহার হয়েছে, কিন্তু delegation করলে শুধু cardGrid এ একবার listener বসানোই যথেষ্ট।

5. What is the difference between preventDefault() and stopPropagation() methods?

উত্তর:
Method	কাজ
preventDefault()	ডিফল্ট আচরণ বন্ধ করে (যেমন form submit বা link redirect)।
stopPropagation()	ইভেন্ট parent এ পৌঁছানো বন্ধ করে।

// preventDefault → ফর্ম submit বন্ধ
document.querySelector('form').addEventListener('submit', e => e.preventDefault());

// stopPropagation → parent listener এ event যাবে না
document.getElementById('child').addEventListener('click', e => e.stopPropagation());

 preventDefault → ডিফল্ট বন্ধ, stopPropagation → bubbling বন্ধ।
