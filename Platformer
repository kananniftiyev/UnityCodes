using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Movement : MonoBehaviour
{
    private float mySpeedx;
    private Vector3 defaultLocalScale;
    private Rigidbody2D myBody;
    public bool onGround; //Zemine Deyib Deymediyini Yoxlamaq.
    private bool canDobuleJump;
    [SerializeField] float currentAttackTime;
    [SerializeField] float mySpeedy;
    [SerializeField] GameObject arrow;
    [SerializeField] float arrowSpeed;
    [SerializeField] bool onAttack;
    [SerializeField] float speed;
    [SerializeField] float defaultAttackTime;
    void Start()
    {
        onAttack = false;
        //Burda Bunlari Shortcut Elememizin Sebebi Hem Rahat Oldugu Ucun Hemde Herdefe Kodu Cagirmamaq Ucundur.
        myBody = GetComponent<Rigidbody2D>();
        defaultLocalScale = transform.localScale;
    }

  
    void Update()
    {
        mySpeedx = Input.GetAxis("Horizontal"); //1 ve -1 arasinda Deyisir.
        myBody.velocity = new Vector2(mySpeedx*speed,myBody.velocity.y);

        KarakterUzTeref();
        Ziplamaq();
        Ates();
/*
Burada ilk once onAttack deye bool deyer yaratdiq ve playerin attackda olub olmadigini kontrol etdik,
Sonra currentAttackTime'i default'a beraber etdikki time menfiye dogru dayanmadan getmesin.
*/
        if(onAttack == true){
            currentAttackTime -= Time.deltaTime;
        }
        else{
            currentAttackTime = defaultAttackTime;
        }
        if (currentAttackTime < 0){
            onAttack = false;
        }
        
    }


    public void KarakterUzTeref(){
        //Burada GetAxis Eger Menfidirse Scale'i -1 Ederek Uzunu Donderirik.
        //Burda Vector3'un Icine Ayri Private Yaradib Qoymamizin Sebebi Oyun Icinde Bunu Istediyimiz Zaman Deyismekdir.
         if(mySpeedx > 0){
            transform.localScale = new Vector3(defaultLocalScale.x,defaultLocalScale.y,defaultLocalScale.z);
        }

        else if(mySpeedx < 0){
            transform.localScale = new Vector3(-defaultLocalScale.x,defaultLocalScale.y,defaultLocalScale.z);
        }
    }

    public void Ziplamaq(){


        //Biz Burada Yerede Olub Olmadigina Baxiriq ve Eger Yerdedise Onda Ziplaya Biler Eksi Teqdirde Yox.
        if(Input.GetKeyDown(KeyCode.Space)){
            if(onGround == true){
           myBody.velocity = new Vector2(myBody.velocity.x, mySpeedy);
           canDobuleJump = true;
       
         }
         else{
             if(canDobuleJump == true){
                myBody.velocity = new Vector2(myBody.velocity.x, 5f);
                canDobuleJump = false;
            }
         }  
        }

    }

    public void Ates(){
        if(Input.GetMouseButtonDown(0)){
         
         if(onAttack == false){
             onAttack = true;
          GameObject okumuz =  Instantiate(arrow,transform.position, Quaternion.identity);
          //Instantiate Yani Prefab Kopyalamaq.
          //(Prefab,Position,Quaternion).
          //Instantiate Bir Game Object Olduguna Gore Onu GameObeye Beraber Edirik.

          if(transform.localScale.x > 0){
              //Burada Eger Bizim Local Scalimiz Saga Ve Ya Sola Olacagini Belirliyirik.
              okumuz.GetComponent<Rigidbody2D>().velocity = new Vector2(arrowSpeed, 0);
          }
          else{
              /*
              Burada Ise Ilk Once Okumuzun Scale'sine Rahat Ulasmaq Ucun Onu transform.localScale e Beraber Etdik.
              */
              Vector3 okumuzScale = okumuz.transform.localScale;
              okumuz.transform.localScale = new Vector3(-okumuzScale.x,okumuzScale.y, okumuzScale.z);

              okumuz.GetComponent<Rigidbody2D>().velocity = new Vector2(-arrowSpeed, 0);
          }
       } }
    }


}
