# Task 6 Boruta

## 1. What parameter name assigns the app password to the specific user?

Answer: `loginName`



We must go to the settings. Next we must add Password App.

<img src="./task_6.png" width="700"/>

Now let's view payload of request.

<img src="./task_6_d.png" width="700"/>


## 2. What is the content of the Fern_flower_ritual_shard4.txt file in Boruta's account?

Answer: Midsummer_Corp{L3ave_an_0ff3r1ng_f0r_th3_spir1ts}

<br> 

Now we must use Postman extension to synchronize cookies and requests with Postman application.

<img src="./task_6_a.png" width="500"/>

Then we must disable automatic redirect in settings.

<img src="./task_6_e.png" width="700"/>

Now we must get Request Token. 

<img src="./task_6_f.png" width="500"/>

And fill it here.

<img src="./task_6_g.png" width="700"/>

We must also find way to avoid security. We can find it in `www\apps\settings\lib\Controller\AuthSettingsController.php`

We can deduce that loginName must have space on the end. 

<img src="./task_6_c.png" width="700"/>

Then the request is send, we will get this output.

<img src="./task_6_b.png" width="700"/>

Now we must open Nextcloud program or something another. Fill server ip.

<img src="./task_6_h.png" width="500"/>

Then we must grant access in browser.

<img src="./task_6_i.png" width="500"/> 

<img src="./task_6_j.png" width="500"/> 

Then we need to use app now.

<img src="./task_6_k.png" width="500"/> 

Then we need to open file explorer.

<img src="./task_6_l.png" width="500"/> 

Here we go. We have file with the answer.

<img src="./task_6_m.png" width="500"/> 