Quiz One
--------

For each multiple choice question, record your answer by pressing the Check Me Button.
You may have as many attempts as you like, but I will only score the first attempt.  If
you do not press the Check Me button your answer will not be recorded.

.. mchoicema:: q1_1
   :answer_a: &lt;h1&gt;
   :answer_b: &lt;p&gt;
   :answer_c: &lt;img&gt;
   :answer_d: &lt;li&gt;
   :correct: a,b,d
   :feedback_a: Yes
   :feedback_b: Yes
   :feedback_c: No, an img tag is an inline element
   :feedback_d: Yes

   Which of the following are HTML block elements.  Select all that apply.

.. mchoicemf:: q1_2
   :answer_a: File Transfer Protocol
   :answer_b: HyperText Markup Language
   :answer_c: Secure Sockets Layer
   :answer_d: HyperText Transfer Protocol
   :correct: d
   :feedback_a: No, FTP is not related to this class.
   :feedback_b: No, HTML is the markup language not the protocol
   :feedback_c: No, SSL is not used
   :feedback_d: Yes

   What is the protocol used in the URL:  ``http://interactivepython.org/index.html``


In the following question, select all of the correct answers for each question.

.. mchoicema:: q1_3
   :answer_a: &lt;h1 class="low"&gt;Hello World&lt;/h1&gt;
   :answer_b: &lt;p class="high"&gt;some text&lt;/p&gt;
   :answer_c: &lt;p&gt;some text&lt;/p&gt;
   :answer_d: &lt;li class="high"&gt;do my homework&lt;/li&gt;
   :answer_e: &lt;p id="high"&gt;some text&lt;/p&gt;
   :correct: b,d
   :feedback_a: This h1 has low class
   :feedback_b: Yes
   :feedback_c: No, the paragraph tag is just a plain paragraph with no class
   :feedback_d: Yes
   :feedback_e: No the selector is matching the class not the id.

   Which of the following will match the CSS selector ``.high``

.. mchoicema:: q1_4
   :answer_a: &lt;h1 class="low"&gt;Hello World&lt;/h1&gt;
   :answer_b: &lt;p class="high"&gt;some text&lt;/p&gt;
   :answer_c: &lt;p&gt;some text&lt;/p&gt;
   :answer_d: &lt;li class="high"&gt;do my homework&lt;/li&gt;
   :answer_e: &lt;p id="high"&gt;some text&lt;/p&gt;
   :correct: b
   :feedback_a: This h1 has low class
   :feedback_b: Yes
   :feedback_c: No, the paragraph tag is just a plain paragraph with no class
   :feedback_d: No, this is an li tag
   :feedback_e: No, this selector is looking for a paragraph with a class of high

   Which of the following will match the CSS selector ``p.high``


.. mchoicema:: q1_5
   :answer_a: &lt;h1 class="low"&gt;Hello World&lt;/h1&gt;
   :answer_b: &lt;p class="high"&gt;some text&lt;/p&gt;
   :answer_c: &lt;p&gt;some text&lt;/p&gt;
   :answer_d: &lt;li class="high"&gt;do my homework&lt;/li&gt;
   :answer_e: &lt;p id="high"&gt;some text&lt;/p&gt;
   :correct: b,c,e
   :feedback_a: No this is an h1 tag
   :feedback_b: Yes
   :feedback_c: Yes
   :feedback_d: No, this is an li tag
   :feedback_e: Yes

   Which of the following will match the CSS selector ``p``

.. mchoicema:: q1_6
   :answer_a: &lt;h1 class="low"&gt;Hello World&lt;/h1&gt;
   :answer_b: &lt;p class="high"&gt;some text&lt;/p&gt;
   :answer_c: &lt;p&gt;some text&lt;/p&gt;
   :answer_d: &lt;li class="high"&gt;do my homework&lt;/li&gt;
   :answer_e: &lt;p id="high"&gt;some text&lt;/p&gt;
   :correct: e
   :feedback_a: No this is an h1 tag
   :feedback_b: No, this selector is matching the id attribute
   :feedback_c: No, this selector is looking for an id
   :feedback_d: No, this selector is matching on the id not the class
   :feedback_e: Yes

   Which of the following will match the CSS selector ``#high``


.. mchoicema:: q1_7
   :answer_a: height
   :answer_b: padding
   :answer_c: border
   :answer_d: margin
   :answer_e: background-color
   :correct: b,c,d
   :feedback_a: No height is an attribute of the content
   :feedback_b: Yes
   :feedback_c: Yes
   :feedback_d: Yes
   :feedback_e: No, background-color is not part of the box model

   Which of the following are properties of the CSS Box Model

For the following questions, I will use your final result.  You can press the Run button as many
times as you like without penalty.  You should also Save your final version.

Fill in the additional HTML needed to make an ordered list of 3 items.  The items should be numbered A, B, and C.

.. actex:: q1_8
   :language: html

   <html>

   </html>

Given the HTML in the activecode below, add the appropriate CSS to style the h1 with a 28pt font, and rgb color consisting of red: 128, blue: 200, green: 99 and the *last* paragraph with a color of orange.

.. actex:: q1_9
   :language: html

   <html>
      <body>
         <h1>Learning about HTML</h1>
         <p>HTML is a fun and easy language to learn</p>
         <h2>Learning about CSS</h2>
         <p class="css"> CSS is fun too, but more challenging than HTML</p>
      </body>
   </html>
