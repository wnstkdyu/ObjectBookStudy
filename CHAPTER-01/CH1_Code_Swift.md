```swift

import Foundation
// MARK: 초대권
class Invitation {
    private(set) var when: Date
    init(when: Date = Date()) {
        self.when = when
    }
}

// MARK: 티켓
class Ticket {
    private(set) var fee: Double
    init(fee: Double) {
        self.fee = fee
    }
}

@objc protocol Wallet {
    func plusAmount(amount: Double)
    @objc optional func minusAmount(amount: Double)
}

// MARK: 사람의 가방, 소지품
class Bag: Wallet {
    private(set) var amount: Double
    private(set) var invitation: Invitation?
    private(set) var ticket: Ticket?

    init(invitation: Invitation? = nil, amount: Double) {
        self.invitation = invitation
        self.amount = amount
    }
    
    var hasInvitation: Bool {
        return invitation != nil
    }
    
    var hasTicket: Bool {
        return ticket != nil
    }
    
    func setTicket(ticket: Ticket) {
        self.ticket = ticket
    }
    
    // 잔액 확인
    func isEnoughMoney(amount: Double) -> Bool {
        return self.amount - amount >= 0
    }
    
    func lackOfMoney() {
        print("잔액이 부족합니다.")
    }
    
    func minusAmount(amount: Double) {
        guard isEnoughMoney(amount: amount) else {
            lackOfMoney()
            return
        }
        
        print("$\(amount) 지불하였습니다")
        self.amount -= amount
    }
    
    func plusAmount(amount: Double) {
        self.amount += amount
    }
    
    func buyAction(ticket: Ticket) -> Double? {
        self.setTicket(ticket: ticket)
        guard hasInvitation else {
            let fee = ticket.fee
            minusAmount(amount: fee)
            return fee
        }
        return nil
    }
}

// MARK: 관람객
class Audience {
    private(set) var bag: Bag
    
    init(bag: Bag) {
        self.bag = bag
    }
    
    func buy(ticket: Ticket?) -> Double? {
        guard let ticket = ticket else { return nil }
        self.bag.buyAction(ticket: ticket)
        return ticket.fee
    }
}

// MARK: 티켓 판매소, 판매원, 극장
class TicketOffice: Wallet {
    private(set) var amount: Double
    private(set) var tickets: [Ticket]
    
    init(amount: Double, tickets: [Ticket]) {
        self.amount = amount
        self.tickets = tickets
    }
    
    func soldOut() {
        print("티켓이 매진되었습니다")
    }
    
    func getTicket() -> Ticket? {
        guard !tickets.isEmpty else {
            soldOut()
            return nil
        }
        return tickets.removeFirst()
    }

    func plusAmount(amount: Double) {
        self.amount += amount
    }
    
    func sellToTicket(audience: Audience) {
        guard let price = audience.buy(ticket: getTicket()) else {
            return
        }
        
        plusAmount(amount: price)
    }
}

class TicketSeller {
    private(set) var ticketOffice: TicketOffice
    init(ticketOffice: TicketOffice) {
        self.ticketOffice = ticketOffice
    }
    
    func sellTo(audience: Audience) {
        ticketOffice.sellToTicket(audience: audience)
    }
}

class Theater {
    private(set) var ticketSeller: TicketSeller
    init(ticketSeller: TicketSeller) {
        self.ticketSeller = ticketSeller
    }
    
    // 누가 들어갔는지
    func enter(audience: Audience) {
        ticketSeller.sellTo(audience: audience)
    }
}

// 영화관
let office = TicketOffice(amount: 1000, tickets: Array(repeating: Ticket(fee: 100), count: 5))
//let office = TicketOffice(amount: 1000, tickets: Array(repeating: Ticket(fee: 100), count: 0)) // 매진 되었습니다.
let seller = TicketSeller(ticketOffice: office)
let theater = Theater(ticketSeller: seller)

// 유저
let bag = Bag(amount: 1000)
let audience = Audience(bag: bag)

let bag2 = Bag(amount: 12)
let audience2 = Audience(bag: bag2)


theater.enter(audience: audience)
theater.enter(audience: audience2) // 잔액이 부족합니다.


```
