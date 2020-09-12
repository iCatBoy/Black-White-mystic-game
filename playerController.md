using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class playercontroller : MonoBehaviour
{
    public float speed;
    float x, sx;
    Rigidbody2D rb;
    int jump;

    private bool isGround,isjumpPad;
    public Transform groundCheck;
    public float checkRadius;
    public LayerMask whatIsGround,jumpPad;
    public float jumpForce;
    void Start()
    {
        rb = GetComponent<Rigidbody2D>();
        sx = transform.localScale.x;
        jump = 2;
    }


    void FixedUpdate()
    {
        isGround = Physics2D.OverlapCircle(groundCheck.position, checkRadius, whatIsGround);
        x = Input.GetAxis("Horizontal");
        isjumpPad = Physics2D.OverlapCircle(groundCheck.position, checkRadius, jumpPad);
        rb.velocity = new Vector2(x * speed, rb.velocity.y);

        if (x > 0)
        {
            transform.localScale = new Vector3(sx, transform.localScale.y, transform.localScale.z);
        }
        if (x< 0)
        {
            transform.localScale = new Vector3(-sx, transform.localScale.y, transform.localScale.z);
        }
    }
    private void Update()
    {
        if(isGround == true )
        {
            jump = 1;
        }
        if(Input.GetButtonDown("Jump") && jump > 0)
        {
            rb.velocity = Vector2.up * jumpForce;
            jump--;
        }
        if (isjumpPad == true)
        {
            jump = 1;
        }
        if (Input.GetButtonDown("Jump") && jump > 0)
        {
            rb.velocity = Vector2.up * (jumpForce + 4);
            jump--;
        }
    }
}
