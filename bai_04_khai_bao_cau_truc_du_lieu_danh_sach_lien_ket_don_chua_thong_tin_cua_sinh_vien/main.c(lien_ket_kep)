#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct {
    char hoten[30];
    int masv;
    float d1, d2, d3;
} Data;

typedef struct tagNode {
    Data infor;
    struct tagNode *prev;
    struct tagNode *next;
} Node;

typedef struct {
    Node *pHead;
    Node *pTail;
    int spt;
} LList;

void initList(LList *L) {
    L->pHead = NULL;
    L->pTail = NULL;
    L->spt = 0;
}

int emptyList(LList L) {
    return L.spt == 0;
}

void insert_Head(LList *L, Data x) {
    Node *pp = (Node*)malloc(sizeof(Node));
    if (pp == NULL) return;

    pp->infor = x;
    pp->prev = NULL;
    pp->next = L->pHead;

    if (emptyList(*L)) {
        L->pTail = pp;
    } else {
        L->pHead->prev = pp;
    }

    L->pHead = pp;
    L->spt++;
}

void insert_Tail(LList *L, Data x) {
    Node *pp = (Node*)malloc(sizeof(Node));
    if (pp == NULL) return;

    pp->infor = x;
    pp->next = NULL;
    pp->prev = L->pTail;

    if (emptyList(*L)) {
        L->pHead = pp;
    } else {
        L->pTail->next = pp;
    }

    L->pTail = pp;
    L->spt++;
}

void delete_Head(LList *L) {
    Node *pp;
    if (emptyList(*L)) {
        printf("Danh sach rong!\n");
        return;
    }

    pp = L->pHead;
    L->pHead = pp->next;

    if (L->pHead == NULL) {
        L->pTail = NULL;
    } else {
        L->pHead->prev = NULL;
    }

    free(pp);
    L->spt--;
}

void delete_Tail(LList *L) {
    Node *pp;
    if (emptyList(*L)) {
        printf("Danh sach rong!\n");
        return;
    }

    pp = L->pTail;
    L->pTail = pp->prev;

    if (L->pTail == NULL) {
        L->pHead = NULL;
    } else {
        L->pTail->next = NULL;
    }

    free(pp);
    L->spt--;
}

void nhap(Data *x) {
    printf("Nhap ma sv: ");
    scanf("%d", &x->masv);

    if (x->masv > 0) {
        printf("Nhap ho ten: ");
        scanf(" %29[^\n]", x->hoten);
        printf("Nhap diem mon 1: ");
        scanf("%f", &x->d1);
        printf("Nhap diem mon 2: ");
        scanf("%f", &x->d2);
        printf("Nhap diem mon 3: ");
        scanf("%f", &x->d3);
    }
}

void in(Data x) {
    printf("Ten: %s, Ma: %d, Diem 1: %.2f, Diem 2: %.2f, Diem 3: %.2f\n",
           x.hoten, x.masv, x.d1, x.d2, x.d3);
}

Node* search(LList L, int ma) {
    Node *pp = L.pHead;
    while (pp != NULL) {
        if (pp->infor.masv == ma) return pp;
        pp = pp->next;
    }
    return NULL;
}

void search_Name(LList L, char ten[]) {
    Node *pp = L.pHead;
    int timThay = 0;

    while (pp != NULL) {
        if (strcmp(pp->infor.hoten, ten) == 0) {
            in(pp->infor);
            timThay = 1;
        }
        pp = pp->next;
    }

    if (timThay == 0) printf("Khong tim thay sinh vien!\n");
}

void delete_Ma(LList *L, int ma) {
    Node *pp = search(*L, ma);

    if (pp == NULL) {
        printf("Khong tim thay ma sinh vien can xoa!\n");
        return;
    }

    if (pp->prev == NULL) L->pHead = pp->next;
    else pp->prev->next = pp->next;

    if (pp->next == NULL) L->pTail = pp->prev;
    else pp->next->prev = pp->prev;

    free(pp);
    L->spt--;
    printf("Da xoa sinh vien co ma %d!\n", ma);
}

void delete_Name(LList *L, char ten[]) {
    Node *pp = L->pHead;
    int dem = 0;

    while (pp != NULL) {
        Node *tiep = pp->next;

        if (strcmp(pp->infor.hoten, ten) == 0) {
            if (pp->prev == NULL) L->pHead = pp->next;
            else pp->prev->next = pp->next;

            if (pp->next == NULL) L->pTail = pp->prev;
            else pp->next->prev = pp->prev;

            free(pp);
            L->spt--;
            dem++;
        }
        pp = tiep;
    }
      if (dem > 0) printf("Da xoa %d sinh vien co ten %s!\n", dem, ten);
    else printf("Khong tim thay ten sinh vien can xoa!\n");
}

void sort_Name(LList *L) {
    Node *pp, *qq;
    Data tam;

    if (L->spt < 2) {
        printf("Danh sach khong du sinh vien de sap xep!\n");
        return;
    }

    for (pp = L->pHead; pp != NULL; pp = pp->next) {
        for (qq = pp->next; qq != NULL; qq = qq->next) {
            if (strcmp(pp->infor.hoten, qq->infor.hoten) > 0) {
                tam = pp->infor;
                pp->infor = qq->infor;
                qq->infor = tam;
            }
        }
    }
    printf("Da sap xep danh sach theo ten!\n");
}

void splitList(LList *L1, LList *L2) {
    Node *pp;
    int n, i;

    if (emptyList(*L1)) {
        printf("Danh sach 1 rong, khong the tach!\n");
        return;
    }
    if (!emptyList(*L2)) {
        printf("Danh sach 2 dang co du lieu, khong the tach!\n");
        return;
    }

    n = L1->spt / 2;
    if (n == 0) n = 1;

    pp = L1->pHead;
    for (i = 1; i < n; i++) pp = pp->next;

    L2->pHead = pp->next;
    L2->pTail = L1->pTail;
    L2->spt = L1->spt - n;

    if (L2->pHead != NULL) L2->pHead->prev = NULL;

    pp->next = NULL;
    L1->pTail = pp;
    L1->spt = n;

    printf("Da tach danh sach thanh 2 danh sach!\n");
}

void mergeList(LList *L1, LList *L2) {
    if (emptyList(*L2)) {
        printf("Danh sach 2 rong, khong co gi de ghep!\n");
        return;
    }

    if (emptyList(*L1)) {
        L1->pHead = L2->pHead;
        L1->pTail = L2->pTail;
        L1->spt = L2->spt;
    } else {
        L1->pTail->next = L2->pHead;
        L2->pHead->prev = L1->pTail;
        L1->pTail = L2->pTail;
        L1->spt += L2->spt;
    }

    initList(L2);
    printf("Da ghep danh sach 2 vao danh sach 1!\n");
}

void processList(LList L) {
    Node *pp = L.pHead;

    if (emptyList(L)) {
        printf("Danh sach rong!\n");
        return;
    }
 while (pp != NULL) {
        in(pp->infor);
        pp = pp->next;
    }
}

void freeList(LList *L) {
    Node *pp;
    while (L->pHead != NULL) {
        pp = L->pHead;
        L->pHead = L->pHead->next;
        free(pp);
    }
    L->pTail = NULL;
    L->spt = 0;
}

int main() {
    LList L, L2;
    Data x;
    int kt = 0, chon, ma;
    Node *pp;
    char ten[30];

    initList(&L);
    initList(&L2);

    do {
        printf("\n===== QUAN LY DANH SACH SINH VIEN =====\n");
        printf("1: Them vao dau danh sach 1\n");
        printf("2: Them vao cuoi danh sach 1\n");
        printf("3: Xoa dau danh sach 1\n");
        printf("4: Xoa cuoi danh sach 1\n");
        printf("5: Tim kiem theo ma\n");
        printf("6: Xoa theo ma\n");
        printf("7: Tim kiem theo ten\n");
        printf("8: Xoa theo ten\n");
        printf("9: Sap xep theo ten\n");
        printf("10: Tach danh sach 1 thanh 2 danh sach\n");
        printf("11: Ghep danh sach 2 vao danh sach 1\n");
        printf("12: Duyet danh sach 1\n");
        printf("13: Duyet danh sach 2\n");
        printf("0: Thoat\n");
        printf("Moi ban chon: ");
        scanf("%d", &chon);

        switch (chon) {
            case 1:
                nhap(&x);
                if (x.masv > 0) insert_Head(&L, x);
                break;
            case 2:
                nhap(&x);
                if (x.masv > 0) insert_Tail(&L, x);
                break;
            case 3:
                delete_Head(&L);
                break;
            case 4:
                delete_Tail(&L);
                break;
            case 5:
                printf("Nhap ma sinh vien can tim: ");
                scanf("%d", &ma);
                pp = search(L, ma);
                if (pp != NULL) in(pp->infor);
                else printf("Khong tim thay sinh vien!\n");
                break;
            case 6:
                printf("Nhap ma sinh vien can xoa: ");
                scanf("%d", &ma);
                delete_Ma(&L, ma);
                break;
            case 7:
                printf("Nhap ten sinh vien can tim: ");
                scanf(" %29[^\n]", ten);
                search_Name(L, ten);
                break;
            case 8:
                printf("Nhap ten sinh vien can xoa: ");
                scanf(" %29[^\n]", ten);
                delete_Name(&L, ten);
                break;
            case 9:
                sort_Name(&L);
                break;
            case 10:
                splitList(&L, &L2);
                break;
            case 11:
                mergeList(&L, &L2);
                break;
            case 12:
                printf("Danh sach 1:\n");
                processList(L);
                break;
            case 13:
                printf("Danh sach 2:\n");
                processList(L2);
                break;
            case 0:
                printf("Bye bye!\n");
                kt = 1;
                break;
            default:
             printf("Lua chon khong hop le!\n");
        }
    } while (kt == 0);
    freeList(&L);
    return 0;
}

