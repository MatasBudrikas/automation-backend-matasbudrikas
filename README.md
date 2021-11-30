# conflictTEST1
const loginURL = 'http://localhost:3000/api/login'

describe('init', function(){
    

    it('Connection test', function () {
        cy.request('http://localhost:3000/api/login').its('status').should('eq', 200)
    })

    it('Login', function(){
        Cypress.Commands.add('loginAuth', () => {
        const userInfo = 
            {"username":"tester01","password":"password01"}
        cy.request({
            method: "POST",
            url: loginURL,
            Headers:{
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(userInfo)
        }).then((response =>{
            expect(response.status).to.eq(200)
            Cypress.env({loginToken:response.body})
             cy.log(response.body)
        }))
    })
        cy.loginAuth()

    })



})
